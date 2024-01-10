## homework_2

Задание 2. A+B.

### Формулировка задания:

Прочитать все комментарии подряд и выполнить все **TODO** в файле ``src/main.cpp`` и ``src/cl/aplusb.cl``.

### Полученные результаты:

<details><summary>Локальный вывод</summary><p>

<pre>
Data generated for n=100000000!
Log:


Kernel average time: 0.0120772+-3.10466e-06 s
GFlops: 8.28009
VRAM bandwidth: 92.5372 GB/s
Result data transfer time: 0.0332998+-0.000274855 s
VRAM -> RAM bandwidth: 11.1871 GB/s

Process finished with exit code 0
</pre>

</p></details>

<details><summary>Вывод Github CI</summary><p>

<pre>

Data generated for n=100000000!
Log:
Compilation started
Compilation done
Linking started
Linking done
Device build started
Device build done
Kernel <aplusb> was successfully vectorized (16)
Kernel <aplusb_wrong> was successfully vectorized (16)
Done.
Kernel average time: 0.0481405+-0.000369545 s
GFlops: 2.07725
VRAM bandwidth: 23.2151 GB/s
Result data transfer time: 3.83333e-06+-3.72678e-07 s
VRAM -> RAM bandwidth: 97181.5 GB/s
</pre>

</p></details>

