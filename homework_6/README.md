## homework_6

Задание 6. Merge sort.

### Формулировка задания:

Реализуйте сортировку слиянием для вещественных чисел. Более простым вариантом будет реализовать бинарный поиск по строчкам и столбцам.

Файлы: ```src/main_merge.cpp``` и ```src/cl/merge.cl```.

### Полученные результаты:

<details><summary>Локальный вывод</summary><p>
<pre>
OpenCL devices:
  Device #0: CPU. Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz. Intel(R) Corporation. Total memory: 15710 Mb
  Device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Using device #1: GPU. NVIDIA GeForce GTX 1050. Total memory: 4040 Mb
Data generated for n=33554432!
CPU: 17.3418+-0.0598856 s
CPU: 1.90292 millions/s
GPU: 0.34465+-0.000124925 s
GPU: 95.7493 millions/s

Process finished with exit code 0
</pre>
</p></details>

<details><summary>Вывод Github CI</summary><p>
<pre>
 OpenCL devices:
  Device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
Using device #0: CPU. Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz. Intel(R) Corporation. Total memory: 6932 Mb
Data generated for n=33554432!
CPU: 3.73361+-0.00673308 s
CPU: 8.83864 millions/s
GPU: 13.7182+-0.0478896 s
GPU: 2.40556 millions/s
</pre>
</p></details>
