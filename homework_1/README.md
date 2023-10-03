## homework_1

Задание 1. Вводное.

### Формулировка задания:

+ Установить OpenCL;
+ Прочитать все комментарии подряд и выполнить все **TODO** в файле ``src/main.cpp``.

### Полученные результаты:

<details><summary>Локальный вывод</summary><p>

<pre>
$ ./enumDevices
Number of OpenCL platforms: 2
Platform #1/2
    Platform name: NVIDIA CUDA
    Platform vendor: NVIDIA Corporation
    Platform number of available devices: 1
    Device #1/1
        Device name: NVIDIA GeForce GTX 1050
        Device type: GPU
        Device memory size, MB: 4040
        Device OpenCL version: OpenCL 3.0 CUDA
        Device maximum clock frequency, MHz: 1493
Platform #2/2
    Platform name: Intel(R) CPU Runtime for OpenCL(TM) Applications
    Platform vendor: Intel(R) Corporation
    Platform number of available devices: 1
    Device #1/1
        Device name: Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz
        Device type: CPU
        Device memory size, MB: 15710
        Device OpenCL version: OpenCL 2.1 (Build 0)
        Device maximum clock frequency, MHz: 2500

The command "./enumDevices" exited with 0.
</pre>

</p></details>

<details><summary>Вывод Github CI</summary><p>

<pre>
Run ./build/enumDevices
Number of OpenCL platforms: 1
Platform #1/1
    Platform name: Intel(R) CPU Runtime for OpenCL(TM) Applications
    Platform vendor: Intel(R) Corporation
    Platform number of available devices: 1
    Device #1/1
        Device name: Intel(R) Xeon(R) Platinum 8272CL CPU @ 2.60GHz
        Device type: CPU
        Device memory size, MB: 6932
        Device OpenCL version: OpenCL 2.1 (Build 0)
        Device maximum clock frequency, MHz: 2600
</pre>

</p></details>

