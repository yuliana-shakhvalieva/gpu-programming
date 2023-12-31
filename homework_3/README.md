## homework_3

Задание 3. Теоретическое задание: параллелизуемость/code divergence/memory coalesced access.

### Формулировка задания:

**1)** Пусть на вход дан сигнал x[n], а на выход нужно дать два сигнала y1[n] и y2[n]:

```
 y1[n] = x[n - 1] + x[n] + x[n + 1]
 y2[n] = y2[n - 2] + y2[n - 1] + x[n]
```

Какой из двух сигналов будет проще и быстрее реализовать в модели массового параллелизма на GPU и почему?

##### Решение: 

Сигнал `y1[n] = x[n - 1] + x[n] + x[n + 1]` будет проще и быстрее реализовать в модели массового параллелизма на GPU, так как каждый элемент можно посчитать независимо от других. То есть при наличии достаточного количества потоков все элементы сигнала `y1` можно получить единовременно, что не получится сделать с сигналом `y2[n] = y2[n - 2] + y2[n - 1] + x[n]`, так как его элементы зависят друг от друга.

**2)** Предположим что размер warp/wavefront равен 32 и рабочая группа делится
 на warp/wavefront-ы таким образом что внутри warp/wavefront
 номер WorkItem по оси x меняется чаще всего, затем по оси y и затем по оси z.

Напоминание: инструкция исполняется (пусть и отмаскированно) в каждом потоке warp/wavefront если хотя бы один поток выполняет эту инструкцию неотмаскированно. Если не все потоки выполняют эту инструкцию неотмаскированно - происходит т.н. code divergence.

Пусть размер рабочей группы (32, 32, 1)

```
int idx = get_local_id(1) + get_local_size(1) * get_local_id(0);
if (idx % 32 < 16)
    foo();
else
    bar();
```

Произойдет ли code divergence? Почему?

##### Решение: 

В описанном примере **не произойдет code divergence**. 
    
По условию: `get_local_size(1)=32`, значит `int idx = get_local_id(1) + 32 * get_local_id(0)`, где `get_local_id(0)` - координата по оси `x`, которая по условию меняется чаще, чем `get_local_id(1)`, координата по `y`.

Так как `get_local_size(1)=32`, то условие `idx % 32` всегда будет равно `get_local_id(1)` при любом `get_local_id(0)`.

Так как размер warp/wavefront совпадает с длиной рабочей группы, то внутри каждого warp/wavefront `get_local_id(1)` будут одинаковыми. То есть внутри warp/wavefront все потоки будут заходить в одну и ту же ветку if. А значит потоки не будут простаивать.

**3)** Как и в прошлом задании предположим что размер warp/wavefront равен 32 и рабочая группа делится
 на warp/wavefront-ы таким образом что внутри warp/wavefront
 номер WorkItem по оси x меняется чаще всего, затем по оси y и затем по оси z.

Пусть размер рабочей группы (32, 32, 1).
Пусть data - указатель на массив float-данных в глобальной видеопамяти идеально выравненный (выравнен по 128 байтам, т.е. data % 128 == 0). И пусть размер кеш линии - 128 байт.

(a)
```
data[get_local_id(0) + get_local_size(0) * get_local_id(1)] = 1.0f;
```

Будет ли данное обращение к памяти coalesced? Сколько кеш линий записей произойдет в одной рабочей группе?

##### Решение: 

Данное обращение к памяти **будет coalesced**, так как обращение идет к индексам, которые расположены друг за другом (`data[get_local_id(0) + 32 * get_local_id(1)] = 1.0f`, где `get_local_id(0)` - координата по оси `x`, которая по условию меняется чаще, чем `get_local_id(1)`, координата по `y`)

Размер кеш-линии составляет `128` байт, значит за один раз в кеш помещается `128/4=32` (`4` - размер `float`) последовательных элементов из массива (размер warp/wavefront), все они используются при следующих обращениях

`32` - кеш линий записей произойдет в одной рабочей группе. 

(b)
```
data[get_local_id(1) + get_local_size(1) * get_local_id(0)] = 1.0f;
```

Будет ли данное обращение к памяти coalesced? Сколько кеш линий записей произойдет в одной рабочей группе?

##### Решение: 

Данное обращение к памяти **не будет coalesced**, так как обращение идет к индексам, которые не расположены друг за другом (`data[get_local_id(1) + 32 * get_local_id(0)] = 1.0f`, где `get_local_id(0)` - координата по оси `x`, которая по условию меняется чаще, чем `get_local_id(1)`, координата по `y`). 
 
Каждый следующий индекс, к которому происходит обращение, на `32` больше предыдущего. 

 Размер кеш-линии составляет `128` байт, значит за один раз в кеш помещается `128/4=32` (`4` - размер `float`) последовательных элементов из массива (размер warp/wavefront), при следующем обращении не используется ни один из элементов, который находится в кеше.

 Необходимо заново загружать, таким образом нужно сделать `32` вызова кеш-линии, а значит всего `32*32 = 1024`

 `1024` - кеш линий записей произойдет в одной рабочей группе. 

(c)
```
data[1 + get_local_id(0) + get_local_size(0) * get_local_id(1)] = 1.0f;
```

Будет ли данное обращение к памяти coalesced? Сколько кеш линий записей произойдет в одной рабочей группе?

##### Решение: 

Данное обращение к памяти **будет coalesced**, так как обращение идет к индексам, которые расположены друг за другом (`data[1 + get_local_id(0) + 32 * get_local_id(1)] = 1.0f`, где `get_local_id(0)` - координата по оси `x`, которая по условию меняется чаще, чем `get_local_id(1)`, координата по `y`)

 Тем не менее из-за сдвига в единицу необходимо загружать сразу 2 кеш линии.

 `64` - кеш линий записей произойдет в одной рабочей группе. 

