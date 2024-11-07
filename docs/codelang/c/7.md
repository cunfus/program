# 并行编程

`OpenMP` 是一种规范，它用了 `#pragma` 和一些函数告诉编译器，在什么时候，怎么开展线程处理。可以用最少的行数，把串行运行的循环，变成线程循环。

```c
#include <stdio.h>
#include <omp.h>
#include <time.h>

int main() {
    long long int count = 0;
    int num_iterations = 1000000000;

    double start_time = omp_get_wtime();

    for (int i = 0; i < num_iterations; i++) {
        count++;
    }

    double end_time = omp_get_wtime();

    printf("Total count: %lld\n", count);
    printf("Execution time: %f seconds\n", end_time - start_time);
    return 0;
}

/*
Total count: 1000000000
Execution time: 0.622888 seconds
*/
```

改为 `OpenMP`，记得编译时带上 `-fopenmp`，

```c
#include <stdio.h>
#include <omp.h>
#include <time.h>

int main() {
    long long int count = 0;
    int num_iterations = 1000000000;

    double start_time = omp_get_wtime();

    #pragma omp parallel
    {
        long long int local_count = 0; // 每个线程的局部计数器

        #pragma omp for
        for (int i = 0; i < num_iterations; i++) {
            local_count++;
        }

        #pragma omp atomic
        count += local_count; 
    }

    double end_time = omp_get_wtime();

    printf("Total count: %lld\n", count);
    printf("Execution time: %f seconds\n", end_time - start_time);
    return 0;
}

/*
Total count: 1000000000
Execution time: 0.111274 seconds
*/
```

- `#pragma omp atomic` 避免竞争条件
- `#pragma omp parallel for`，表示循环分解为多个段。

分解的段数大小可以从环境变量中获取，`export OMP_NUM_THREADS=N`，或在程序开始时设置好，

```c
#include <omp.h>
omp_set_num_threads(N);
// omp_set_num_threads(omp_get_num_procs());
```

容易出现的问题，这个地方容易出现的问题是，当你尝试批量运行含有 openmp 的程序时，虽然每个进程都有自己的虚拟内存空间，但它们共享着系统资源啊，比如CPU、内存、和 IO。这可能导致资源的竞争，从而使性能下降，而不是提升。