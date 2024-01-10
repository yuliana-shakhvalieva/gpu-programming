## homework_4

Задание 4. Фрактал Мандельброта. Сумма чисел.

### Формулировка задания:

#### Задание 4.1. Фрактал Мандельброта

Реализуйте расчет фрактала Мандельброта на OpenCL.

Файлы: ```src/main_mandelbrot.cpp``` и ```src/cl/mandelbrot.cl```.

#### Задание 4.2. Суммирование чисел

1. Реализуйте несколько методов суммирования чисел на OpenCL:

+ Суммирование с глобальным атомарным добавлением (просто как бейзлайн);

+ Суммирование с циклом;

+ Суммирование с циклом и coalesced доступом;

+ Суммирование с локальной памятью и главным потоком;

+ Суммирование с деревом.

2. Посмотрите на результаты производительности и попробуйте их проанализировать с учетом своего железа, обсуждения на лекции и ожиданий, какая версия должна была бы стать самой быстрой. 

Файл: ```src/main_sum.cpp```.

### Полученные результаты:

<details><summary>Локальный вывод sum</summary><p>

<pre>
CPU:     0.261253+-0.00137017 s
CPU:     382.771 millions/s

CPU OMP: 0.0832528+-0.00376301 s
CPU OMP: 1201.16 millions/s

OpenCL devices:
  Device #0: CPU. Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz. Intel(R) Corporation. Total memory: 15710 Mb
  Device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Using device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
GPU sum1_baseline_atomic_add: 0.00842133+-1.19536e-05 s
GPU sum1_baseline_atomic_add: 11874.6 millions/s

GPU sum2_with_cycle: 0.0183665+-0.000700892 s
GPU sum2_with_cycle: 5444.7 millions/s

GPU sum3_with_cycle_coalesced: 0.00391333+-6.54896e-06 s
GPU sum3_with_cycle_coalesced: 25553.7 millions/s

GPU sum4_local_mem_and_main_thread: 0.0102308+-4.7052e-06 s
GPU sum4_local_mem_and_main_thread: 9774.37 millions/s

GPU sum5_with_tree: 0.0142205+-0.000457022 s
GPU sum5_with_tree: 7032.1 millions/s


Process finished with exit code 0
</pre>

</p></details>

<details><summary>Локальный вывод mandelbrot</summary><p>

<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz. Intel(R) Corporation. Total memory: 15710 Mb
  Device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Using device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
CPU: 1.24077+-0.0312487 s
CPU: 8.05954 GFlops
    Real iterations fraction: 56.2638%
GPU: 0.0139722+-4.37851e-05 s
GPU: 715.709 GFlops
    Real iterations fraction: 56.2638%
GPU vs CPU average results difference: 0.942446%

Process finished with exit code 0
</pre>

</p></details>

<details><summary>Вывод Github CI sum</summary><p>

<pre>
CPU:     0.064586+-0.000309703 s
CPU:     1548.32 millions/s

CPU OMP: 0.0272323+-0.00010938 s
CPU OMP: 3672.11 millions/s

OpenCL devices:
  Device #0: CPU. Intel(R) Xeon(R) Platinum 8272CL CPU @ 2.60GHz. Intel(R) Corporation. Total memory: 6932 Mb
Using device #0: CPU. Intel(R) Xeon(R) Platinum 8272CL CPU @ 2.60GHz. Intel(R) Corporation. Total memory: 6932 Mb
GPU sum1_baseline_atomic_add: 1.66992+-0.00862323 s
GPU sum1_baseline_atomic_add: 59.8833 millions/s

GPU sum2_with_cycle: 0.0828658+-3.58907e-05 s
GPU sum2_with_cycle: 1206.77 millions/s

GPU sum3_with_cycle_coalesced: 0.0362995+-7.97679e-05 s
GPU sum3_with_cycle_coalesced: 2754.86 millions/s

GPU sum4_local_mem_and_main_thread: 0.0792885+-9.32787e-05 s
GPU sum4_local_mem_and_main_thread: 1261.22 millions/s

GPU sum5_with_tree: 0.198291+-0.000301444 s
GPU sum5_with_tree: 504.31 millions/s
</pre>

</p></details>

<details><summary>Вывод Github CI mandelbrot</summary><p>

<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Xeon(R) Platinum 8272CL CPU @ 2.60GHz. Intel(R) Corporation. Total memory: 6932 Mb
Using device #0: CPU. Intel(R) Xeon(R) Platinum 8272CL CPU @ 2.60GHz. Intel(R) Corporation. Total memory: 6932 Mb
CPU: 1.55937+-0.00598649 s
CPU: 6.41286 GFlops
    Real iterations fraction: 56.2638%
GPU: 0.111667+-0.000253143 s
GPU: 89.5517 GFlops
    Real iterations fraction: 56.2638%
GPU vs CPU average results difference: 0.942446%
</pre>

</p></details>

Cамым быстрым методом на обоих платформах оказался метод суммирования с циклом и coalesced доступом. При чем отрыв от ближайших соперников был значительным в обоих случаях. Наблюдается интересная картина с бейзлайновым методом с атомарным добавлением: кажется, что этот метод самый простой, без какой бы то ни было оптимизации, тем не менее он занимает второе место по скорости в локальном выводе. Тем не менее на Github CI описываемый метод ожидаемо занимает последнюю позицию. Похожая ситуация и с суммированием с циклом: локально этот способ показал наихудший результат, а на Github CI он занял в второе место. 

В общем и целом, можно сделать вывод о том, что скорость сильно зависит не только от способа вычислений, но и от железа их производящего.
