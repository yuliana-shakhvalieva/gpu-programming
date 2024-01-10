## homework_7

Задание 7. Bitonic sort, prefix sum.

### Формулировка задания:

#### Задание 7.1. Bitonic sort

Реализуйте битоническую сортировку для вещественных чисел.

Файлы: ```src/main_bitonic.cpp``` и ```src/cl/bitonic.cl```.

#### Задание 7.2. Prefix sum

Реализуйте алгоритм подсчета префиксных сумм в модели массового параллелизма.

Файлы: ```src/main_prefix_sum.cpp``` и ```src/cl/prefix_sum.cl```.

### Полученные результаты:

<details><summary>Локальный вывод bitonic</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz. Intel(R) Corporation. Total memory: 15710 Mb
  Device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Using device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Data generated for n=33554432!
CPU: 16.4904+-0.0221597 s
CPU: 2.00116 millions/s
GPU: 0.738486+-0.000109776 s
GPU: 44.686 millions/s

Process finished with exit code 0
</pre>
</p></details>

<details><summary>Вывод Github CI bitonic</summary><p>
<pre>
  OpenCL devices:
  Device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v3 @ 2.40GHz. Intel(R) Corporation. Total memory: 6932 Mb
Using device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v3 @ 2.40GHz. Intel(R) Corporation. Total memory: 6932 Mb
Data generated for n=33554432!
CPU: 3.55478+-0.020485 s
CPU: 9.28327 millions/s
GPU: 32.2984+-0.148596 s
GPU: 1.02172 millions/s
</pre>
</p></details>

<details><summary>Локальный вывод prefix_sum</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz. Intel(R) Corporation. Total memory: 15710 Mb
  Device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Using device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
______________________________________________
n=4096 values in range: [0; 1023]
CPU: 3.6e-05+-5.7735e-07 s
CPU: 113.778 millions/s
GPU: 0.000132+-1.91485e-06 s
GPU: 31.0303 millions/s
______________________________________________
n=16384 values in range: [0; 1023]
CPU: 0.000143833+-3.72678e-07 s
CPU: 113.91 millions/s
GPU: 0.0001865+-1.25831e-06 s
GPU: 87.8499 millions/s
______________________________________________
n=65536 values in range: [0; 1023]
CPU: 0.000582167+-1.77169e-06 s
CPU: 112.573 millions/s
GPU: 0.000345667+-5.61743e-06 s
GPU: 189.593 millions/s
______________________________________________
n=262144 values in range: [0; 1023]
CPU: 0.00241167+-2.59594e-05 s
CPU: 108.698 millions/s
GPU: 0.00106883+-3.50115e-05 s
GPU: 245.262 millions/s
______________________________________________
n=1048576 values in range: [0; 1023]
CPU: 0.0102732+-0.00050237 s
CPU: 102.069 millions/s
GPU: 0.003795+-4.42869e-05 s
GPU: 276.305 millions/s
______________________________________________
n=4194304 values in range: [0; 511]
CPU: 0.0383037+-0.000213291 s
CPU: 109.501 millions/s
GPU: 0.0146377+-4.59081e-05 s
GPU: 286.542 millions/s
______________________________________________
n=16777216 values in range: [0; 127]
CPU: 0.201251+-0.0318618 s
CPU: 83.3647 millions/s
GPU: 0.0683747+-0.00513133 s
GPU: 245.372 millions/s

Process finished with exit code 0
</pre>
</p></details>

<details><summary>Вывод Github CI prefix_sum</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
Using device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
______________________________________________
n=4096 values in range: [0; 1023]
CPU: 9.33333e-06+-4.71405e-07 s
CPU: 438.857 millions/s
GPU: 0.000227333+-8.76863e-06 s
GPU: 18.0176 millions/s
______________________________________________
n=16384 values in range: [0; 1023]
CPU: 3.8e-05+-0 s
CPU: 431.158 millions/s
GPU: 0.000533667+-1.48399e-05 s
GPU: 30.7008 millions/s
______________________________________________
n=65536 values in range: [0; 1023]
CPU: 0.000152+-0 s
CPU: 431.158 millions/s
GPU: 0.00172967+-4.08316e-05 s
GPU: 37.8894 millions/s
______________________________________________
n=262144 values in range: [0; 1023]
CPU: 0.000609+-1.1547e-06 s
CPU: 430.45 millions/s
GPU: 0.006755+-4.3566e-05 s
GPU: 38.8074 millions/s
______________________________________________
n=1048576 values in range: [0; 1023]
CPU: 0.002473+-2.16872e-05 s
CPU: 424.01 millions/s
GPU: 0.0273615+-0.000435211 s
GPU: 38.323 millions/s
______________________________________________
n=4194304 values in range: [0; 511]
CPU: 0.00993033+-3.80949e-05 s
CPU: 422.373 millions/s
GPU: 0.114659+-0.00107402 s
GPU: 36.5808 millions/s
______________________________________________
n=16777216 values in range: [0; 127]
CPU: 0.0401963+-0.000404386 s
CPU: 417.382 millions/s
GPU: 0.495183+-0.00286809 s
GPU: 33.8808 millions/s
</pre>
</p></details>

