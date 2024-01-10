## homework_5

Задание 5. Транспонирование матрицы, умножение матриц.

### Формулировка задания:

#### Задание 5.1. Транспонирование матрицы

Реализуйте транспонирование матрицы таким образом, чтобы доступ и на чтение и на запись к глобальной видеопамяти был coalesced. (т.е. через локальную память).

Файлы: ```src/main_matrix_transpose.cpp``` и ```src/cl/matrix_transpose.cl```.

#### Задание 5.2. Умножение матриц

1. Реализуйте несколько методов умножения матриц на OpenCL:

+ Наивное умножение матриц через глобальную память;

+ Умножение матриц через локальную память;

+ Умножение матриц через локальную память с большим количеством работы на один воркайтем.

2. Сравните производительность трех реализаций.

Файлы: ```src/main_matrix_multiplication.cpp``` и ```src/cl/matrix_multiplication.cl```.

### Полученные результаты:

<details><summary>Локальный вывод matrix_transpose</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz. Intel(R) Corporation. Total memory: 15710 Mb
  Device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Using device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Data generated for M=1024, K=1024
GPU: 0.000133167+-3.72678e-07 s
GPU: 7874.16 millions/s

Process finished with exit code 0
</pre>
</p></details>

<details><summary>Локальный вывод matrix_multiplication</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz. Intel(R) Corporation. Total memory: 15710 Mb
  Device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Using device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Data generated for M=1024, K=1024, N=1024
CPU: 17.2414+-0.107135 s
CPU: 0.116 GFlops

matmul1_naive
GPU: 0.0224722+-0.000642007 s
GPU: 88.999 GFlops
Average difference: 0.000149043%

matmul2_local_memory
GPU: 0.00843383+-0.000346526 s
GPU: 237.14 GFlops
Average difference: 0.000149043%

matmul3_local_memory_more_per_thread
GPU: 0.00648617+-6.61858e-06 s
GPU: 308.349 GFlops
Average difference: 0.000149043%

Process finished with exit code 0
</pre>
</p></details>


<details><summary>Вывод Github CI matrix_transpose</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
Using device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
Data generated for M=1024, K=1024
GPU: 0.00228183+-0.00019718 s
GPU: 459.532 millions/s
</pre>
</p></details>


<details><summary>Вывод Github CI matrix_multiplication</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
Using device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
Data generated for M=1024, K=1024, N=1024
CPU: 2.65245+-0.0326406 s
CPU: 0.75402 GFlops

matmul1_naive
GPU: 0.186577+-0.00246454 s
GPU: 10.7194 GFlops
Average difference: 0.000149043%

matmul2_local_memory
GPU: 0.20392+-0.00407951 s
GPU: 9.80775 GFlops
Average difference: 0.000149043%

matmul3_local_memory_more_per_thread
GPU: 0.343687+-0.00853186 s
GPU: 5.81925 GFlops
Average difference: 0.000149043%
</pre>
</p></details>

Локально получены ожидаемые результаты: наивный метод самый медленный, а метод с локальной памятью с большим количеством работы на один воркайтем - самый быстрый. При этом метод с локальной памятью в 3 раза быстрее просто наивной реализации (это объясняется coalesced memory access). При увеличении количества работы на один воркайтем ускорение чуть менее значительное: в 1,3 раза.

Что касается GitHub CI, то полученные результаты противоположны локальным результатам. Здесь наивная реализация является самой быстрой, а метод с локальной памятью с большим количеством работы на один воркайтем - самый медленный.
