# 011：TinyEngine与并行处理 🚀

在本节课中，我们将学习如何高效地编程资源受限的设备，特别是针对神经网络的推理和训练。我们将探讨一系列并行计算技术，包括循环优化、多线程、SIMD编程和CUDA编程，以及几种关键的推理优化方法。这些知识对于在本地设备（如笔记本电脑）上部署大型语言模型至关重要。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_1.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_3.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_4.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_6.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_7.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_9.png)

---

![](img/6cdea097a850d3f9a9f2ad163674c9d7_11.png)

## 1. 边缘AI的约束与动机

![](img/6cdea097a850d3f9a9f2ad163674c9d7_13.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_14.png)

上一节我们介绍了课程背景，本节中我们来看看边缘AI（TinyML）面临的核心挑战。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_16.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_17.png)

边缘AI在智能手机、汽车、机器人和智能办公室等领域有广泛应用。然而，边缘设备（如微控制器）的计算资源非常有限。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_19.png)

以下是不同设备的资源对比：

![](img/6cdea097a850d3f9a9f2ad163674c9d7_20.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_21.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_23.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_24.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_26.png)

*   **云GPU/服务器**：内存可达数百GB，算力达数千TOPS/秒。
*   **桌面设备**：内存约8-24GB，算力约30 TOPS/秒。
*   **移动设备**：内存约8-24GB，算力约数百GOPS/秒。
*   **微控制器**：内存仅约300KB，算力仅约数百MOPS/秒。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_28.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_30.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_31.png)

资源差异可达数个数量级，这促使我们必须高效地编程这些设备。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_33.png)

以MacBook Pro与微控制器对比为例：

![](img/6cdea097a850d3f9a9f2ad163674c9d7_35.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_36.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_37.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_39.png)

| 资源项 | 微控制器 | MacBook Pro |
| :--- | :--- | :--- |
| **CPU核心数** | 1 | 20 |
| **时钟频率** | 200 MHz | 3 GHz |
| **GPU/神经引擎** | 无 | 有 |
| **L1缓存** | 8 KB | 大 |
| **L2/L3缓存** | 无 | 有 |
| **内存容量** | 数百KB | 64 GB |
| **操作系统** | 无（需自行管理内存） | 有 |

![](img/6cdea097a850d3f9a9f2ad163674c9d7_41.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_42.png)

此外，理解内存层次结构（Memory Hierarchy）至关重要。从寄存器、各级缓存到主存和存储，容量递增，但访问延迟也急剧增加。我们的优化目标是尽可能让数据停留在高速缓存中，避免访问慢速的DRAM。

**公式**：`访问延迟：寄存器 < L1缓存 < L2缓存 < L3缓存 < 主存 < 存储`

![](img/6cdea097a850d3f9a9f2ad163674c9d7_44.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_46.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_48.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_49.png)

---

![](img/6cdea097a850d3f9a9f2ad163674c9d7_51.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_52.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_53.png)

## 2. 循环优化技术

给定上述约束，我们需要高效地利用并行性来加速神经网络推理。循环优化是基础且关键的技术，因为矩阵乘法和卷积等核心操作本质上是嵌套循环。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_55.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_57.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_58.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_60.png)

我们的主要优化目标是：
1.  **优化局部性**：提高缓存命中率。
2.  **减少分支开销**：尽量避免分支预测错误。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_62.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_63.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_65.png)

以下是三种核心的循环优化技术。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_67.png)

### 2.1 循环重排

![](img/6cdea097a850d3f9a9f2ad163674c9d7_69.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_71.png)

循环重排通过改变嵌套循环的顺序来优化数据访问的局部性。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_73.png)

考虑一个朴素的N×N矩阵乘法实现：
```c
for (int i = 0; i < N; i++) {
    for (int j = 0; j < N; j++) {
        for (int k = 0; k < N; k++) {
            C[i][j] += A[i][k] * B[k][j]; // IJK顺序
        }
    }
}
```
在`IJK`顺序下，矩阵`A`按行访问（局部性好），但矩阵`B`按列访问。由于内存是行优先存储的，按列访问`B`会导致缓存行（Cache Line）利用率低，频繁发生缓存缺失。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_75.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_77.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_79.png)

解决方案是将循环顺序改为`IKJ`：
```c
for (int i = 0; i < N; i++) {
    for (int k = 0; k < N; k++) {
        for (int j = 0; j < N; j++) {
            C[i][j] += A[i][k] * B[k][j]; // IKJ顺序
        }
    }
}
```
现在，`A`和`B`都按行访问，提高了`B`的缓存局部性。虽然输出矩阵`C`的局部性可能变差，但`B`的优化收益通常更大。实测中，这种简单的改变可带来约12倍的加速（从24000毫秒降至约2000毫秒）。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_81.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_83.png)

### 2.2 循环分块

当数据远大于缓存容量时（例如4K×4K矩阵），我们需要使用循环分块技术。它将大循环迭代空间分割成多个小块（Tile），确保每个小块的数据能完全放入缓存，从而被重复利用。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_85.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_86.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_88.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_89.png)

以下是分块技术的演进：

![](img/6cdea097a850d3f9a9f2ad163674c9d7_91.png)

1.  **基线（无分块）**：三个嵌套循环（`IJK`），`B`矩阵的访存足迹为`N²`。
2.  **单维度分块**：增加第四个循环，对`J`维度分块。`B`矩阵的访存足迹减少为`N * TILE_SIZE`。
3.  **双维度分块**：增加第五个循环，对`K`维度也分块。`B`矩阵的访存足迹减少为`TILE_SIZE²`。
4.  **全维度分块**：增加第六个循环，对`I`维度也分块。此时`A`、`B`、`C`三个矩阵的访存足迹都约为`TILE_SIZE²`。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_93.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_94.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_95.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_97.png)

**如何确定分块大小（TILE_SIZE）？**
目标是让`TILE_SIZE²`小于缓存容量。对于多级缓存（如L1、L2），可以进行多层次分块，让小块适应L1缓存，让由多个小块组成的更大块适应L2缓存。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_98.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_100.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_102.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_103.png)

通过六层循环分块，矩阵乘法时间可以从24000毫秒降至1200毫秒，实现19倍加速。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_105.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_107.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_109.png)

### 2.3 循环展开

![](img/6cdea097a850d3f9a9f2ad163674c9d7_111.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_112.png)

处理器中的分支预测错误代价高昂。循环展开通过复制循环体多次来减少循环迭代次数，从而减少分支判断和指针运算的开销。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_114.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_115.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_117.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_118.png)

朴素的内部循环：
```c
for (int k = 0; k < N; k++) {
    C[i][j] += A[i][k] * B[k][j];
}
```
展开4次后：
```c
for (int k = 0; k < N; k += 4) {
    C[i][j] += A[i][k] * B[k][j];
    C[i][j] += A[i][k+1] * B[k+1][j];
    C[i][j] += A[i][k+2] * B[k+2][j];
    C[i][j] += A[i][k+3] * B[k+3][j];
}
```
**优点**：
*   分支测试次数减少为1/4。
*   指针运算次数减少为1/4。
**缺点**：
*   代码体积增大（变为4倍）。
*   需要处理循环次数不是展开因子整数倍的情况。

循环展开通常与分块结合使用。实测中，结合展开可进一步将时间从8000毫秒降至更低。现代编译器能自动进行部分循环优化，但对于特定尺寸的矩阵，手工优化往往更有效。

---

## 3. SIMD（单指令多数据）编程

![](img/6cdea097a850d3f9a9f2ad163674c9d7_120.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_121.png)

神经网络计算是高度并行的。SIMD允许一条指令同时处理多个数据元素，显著提升计算吞吐量和能效。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_123.png)

### 3.1 SIMD核心概念

![](img/6cdea097a850d3f9a9f2ad163674c9d7_125.png)

*   **标量寄存器**：存储单个数据元素。
*   **向量寄存器**：存储多个数据元素（如128位寄存器可存放4个32位浮点数）。
*   **向量操作**：一条指令对整个向量寄存器进行操作。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_127.png)

**公式**：`SIMD加速比 ≈ 向量宽度（如4）`

### 3.2 使用Intrinsics进行SIMD编程

以下是使用X86 SSE intrinsics和ARM NEON intrinsics实现点积运算的对比：

![](img/6cdea097a850d3f9a9f2ad163674c9d7_129.png)

**标量实现（SISD）**：
```c
float c = 0;
for (int k = 0; k < N; k++) {
    c += a[k] * b[k];
}
```

**X86 SSE Intrinsics实现（处理4个元素）**：
```c
__m128 sum = _mm_setzero_ps();
for (int k = 0; k < N; k += 4) {
    __m128 vecA = _mm_load_ps(&a[k]); // 加载4个单精度浮点数
    __m128 vecB = _mm_load_ps(&b[k]);
    sum = _mm_add_ps(sum, _mm_mul_ps(vecA, vecB));
}
// 将sum中的4个结果水平相加得到最终c
```

![](img/6cdea097a850d3f9a9f2ad163674c9d7_131.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_132.png)

**ARM NEON Intrinsics实现**：
```c
float32x4_t sum = vdupq_n_f32(0.0f);
for (int k = 0; k < N; k += 4) {
    float32x4_t vecA = vld1q_f32(&a[k]);
    float32x4_t vecB = vld1q_f32(&b[k]);
    sum = vmlaq_f32(sum, vecA, vecB); // 乘加操作
}
// 同样需要归约得到最终结果
```
通过SIMD intrinsics，我们可以重写矩阵乘法的内循环，一次处理4个元素，从而获得显著加速。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_133.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_135.png)

---

![](img/6cdea097a850d3f9a9f2ad163674c9d7_137.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_139.png)

## 4. 多线程编程

多线程允许在单个进程内并发执行多个线程，充分利用多核CPU。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_141.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_142.png)

### 4.1 多线程基础

*   **共享**：同一进程的线程共享代码段、数据段和打开的文件。
*   **私有**：每个线程有自己的寄存器、栈和程序计数器。
*   **优势**：
    *   **提升性能**：线程可同时在多个CPU核心上执行。
    *   **提高资源利用率**：当一个线程因I/O阻塞时，CPU可切换到其他线程执行。

### 4.2 使用Pthread进行矩阵乘法并行化

一个直观的并行化策略是按行划分工作。每个线程负责计算输出矩阵`C`的一部分行。

以下是使用Pthread的关键步骤：

1.  **创建线程**：`pthread_create(&threads[t], NULL, matmul_thread_func, &args[t])`
2.  **定义线程函数**：每个线程根据其ID计算自己负责的行范围（`start_row` 到 `end_row`），然后执行该范围内的三层循环乘法。
3.  **同步等待**：`pthread_join(threads[t], NULL)` 等待所有线程完成。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_144.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_146.png)

使用4个线程，矩阵乘法时间可以从24000毫秒降至约5800毫秒，实现4倍以上的加速。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_148.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_150.png)

### 4.3 使用OpenMP简化并行编程

OpenMP通过编译器指令简化了共享内存并行编程。

使用OpenMP并行化矩阵乘法的`I`循环非常简单：
```c
#pragma omp parallel for
for (int i = 0; i < N; i++) {
    for (int j = 0; j < N; j++) {
        for (int k = 0; k < N; k++) {
            C[i][j] += A[i][k] * B[k][j];
        }
    }
}
```
只需一行指令，编译器会自动处理线程创建、工作分配和同步。OpenMP代码比Pthread更简洁、更便携。

---

## 5. CUDA编程

GPU提供了远超CPU的并行吞吐量和内存带宽。CUDA是NVIDIA推出的通用GPU计算平台和编程模型。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_152.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_154.png)

### 5.1 CUDA线程层次与执行模型

![](img/6cdea097a850d3f9a9f2ad163674c9d7_155.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_157.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_159.png)

CUDA采用两层线程层次：
*   **网格**：由多个线程块组成。
*   **线程块**：由多个线程组成。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_161.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_163.png)

线程ID是三维的，便于处理ND数组。以下代码启动一个执行矩阵加法的内核：
```c
dim3 threadsPerBlock(4, 3); // 每个块有4x3=12个线程
dim3 numBlocks((Nx + threadsPerBlock.x - 1) / threadsPerBlock.x,
               (Ny + threadsPerBlock.y - 1) / threadsPerBlock.y); // 计算需要的块数
matrixAdd<<<numBlocks, threadsPerBlock>>>(d_A, d_B, d_C, Nx, Ny);
```
单行代码即可启动大量线程（如`numBlocks.x * numBlocks.y * 12`个）。每个线程通过`blockIdx`和`threadIdx`确定自己负责处理输入矩阵中的哪个元素。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_164.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_166.png)

### 5.2 CUDA内存模型

![](img/6cdea097a850d3f9a9f2ad163674c9d7_168.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_170.png)

*   **主机与设备**：CPU（主机）和GPU（设备）有独立的地址空间，数据必须显式复制。
    ```c
    float *d_A;
    cudaMalloc(&d_A, size); // 在设备上分配内存
    cudaMemcpy(d_A, h_A, size, cudaMemcpyHostToDevice); // 主机->设备
    cudaMemcpy(h_C, d_C, size, cudaMemcpyDeviceToHost); // 设备->主机
    cudaFree(d_A);
    ```
*   **设备内存层次**：
    *   **全局内存**：所有线程可读写，速度慢。
    *   **共享内存**：同一线程块内的线程可读写，速度快。
    *   **本地内存**：每个线程私有，速度慢。

### 5.3 使用CUDA加速矩阵乘法

通过将矩阵分块，并利用共享内存来存储数据块，可以极大减少对全局内存的访问。核心步骤包括：
1.  每个线程块将`A`和`B`的一个瓦片加载到共享内存。
2.  线程块内同步（`__syncthreads()`）。
3.  每个线程使用共享内存中的数据计算部分结果。
4.  将最终结果写回全局内存。

在GTX 1080 Ti GPU上，CUDA内核计算本身仅需约6毫秒，整体过程约200毫秒，相比CPU单线程实现有巨大加速。需要注意的是，内核启动本身有开销，因此应尽可能进行**内核融合**，将多个操作（如矩阵乘法和激活函数）合并到单个内核中执行。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_172.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_174.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_176.png)

### 5.4 Tensor Core

![](img/6cdea097a850d3f9a9f2ad163674c9d7_178.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_179.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_181.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_183.png)

现代GPU（如Volta架构及以后）引入了Tensor Core，专门用于加速矩阵乘累加运算，尤其针对低精度数据类型（如FP16, INT8, INT4）。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_185.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_187.png)

*   **性能对比**：Tensor Core的吞吐量远超传统的CUDA Core。例如，在H100上，对于大矩阵运算，Tensor Core的吞吐量可达CUDA Core的60倍以上。
*   **编程模型**：使用WMMA（Warp Matrix Multiply Accumulate）API。即使实际矩阵很大，也可以通过将输入输出分解为16x16等小块，多次调用WMMA intrinsic来完成计算。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_189.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_190.png)

---

![](img/6cdea097a850d3f9a9f2ad163674c9d7_192.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_194.png)

## 6. 推理优化技术

前述技术是函数保留的优化，即不改变数学运算本身。本节介绍几种针对卷积运算的具体优化方法。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_196.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_197.png)

### 6.1 Im2Col卷积

![](img/6cdea097a850d3f9a9f2ad163674c9d7_199.png)

卷积运算有六层循环，而矩阵乘法高度优化。Im2Col将卷积转换为矩阵乘法。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_201.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_203.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_205.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_207.png)

**原理**：
1.  将输入特征图的每个局部感受野（例如3x3）展开成一行，堆叠成一个大矩阵。
2.  将卷积核展开成一列（对于多个输出通道，则是多列）。
3.  对这两个矩阵执行矩阵乘法，结果即为输出特征图。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_209.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_211.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_213.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_215.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_217.png)

**公式**：`输出 = Im2Col(输入) * 卷积核（重排后）`

![](img/6cdea097a850d3f9a9f2ad163674c9d7_219.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_221.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_223.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_225.png)

**优点**：实现简单，可利用高度优化的GEMM库。
**缺点**：需要额外的内存来存储展开后的矩阵，存在数据冗余。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_226.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_228.png)

### 6.2 原地深度可分离卷积

![](img/6cdea097a850d3f9a9f2ad163674c9d7_230.png)

深度可分离卷积（如MobileNet中的）由逐通道卷积和逐点卷积组成。逐通道卷积每个输入通道独立卷积。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_232.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_233.png)

**朴素实现**：需要分配与输入大小相同的临时输出缓冲区，总内存占用为`2 * C * H * W`。
**原地优化**：只分配一个通道大小的临时缓冲区。计算一个通道时，将结果存于此缓冲区，再写回输出的对应通道位置。内存占用降至`(1 + C) * H * W`，显著降低。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_235.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_236.png)

### 6.3 内存布局：NHWC vs NCHW

![](img/6cdea097a850d3f9a9f2ad163674c9d7_238.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_240.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_241.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_243.png)

数据在内存中的布局方式对性能有巨大影响。
*   **NCHW**：`[批次， 通道， 高， 宽]`，通道连续存储。
*   **NHWC**：`[批次， 高， 宽， 通道]`，同一空间位置的通道值连续存储。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_244.png)

**选择策略**：
*   **逐点卷积（1x1）**：偏好**NHWC**。因为计算时需要同时访问同一空间位置的所有通道，NHWC布局下这些数据是连续的。
*   **逐通道卷积**：偏好**NCHW**。因为每个通道独立计算，NCHW布局下单个通道的数据是连续存储的，访问效率高。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_246.png)

### 6.4 Winograd卷积

![](img/6cdea097a850d3f9a9f2ad163674c9d7_248.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_250.png)

Winograd是一种快速卷积算法，通过增加加法操作来减少乘法次数，对于小尺寸卷积核（如3x3）尤其有效。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_252.png)

**原理**：
1.  使用预定义的变换矩阵`G`、`B`、`A`（其元素仅为0、1、-1、1/2等），分别对滤波器、输入数据和输出数据进行变换。乘1/2可用移位实现，因此变换本身计算代价低。
2.  在变换后的空间进行**逐元素乘法**（而非卷积）。
3.  将结果变换回来。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_254.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_256.png)

**效果**：对于计算4个输出点的3x3卷积，普通卷积需要`4 * 9 = 36`次乘加。Winograd F(2x2, 3x3)仅需要`4 * 4 = 16`次乘加，减少了约2.25倍的乘法运算。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_258.png)

**公式**（简化表示）：
`Y = A^T * [(G * g * G^T) ⊙ (B^T * d * B)] * A`
其中`⊙`表示逐元素乘法，`g`是滤波器，`d`是输入数据。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_260.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_261.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_263.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_264.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_266.png)

---

![](img/6cdea097a850d3f9a9f2ad163674c9d7_268.png)

## 7. 总结与应用

![](img/6cdea097a850d3f9a9f2ad163674c9d7_270.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_271.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_273.png)

![](img/6cdea097a850d3f9a9f2ad163674c9d7_274.png)

本节课我们一起学习了在资源受限环境下进行高效神经网络推理的全套技术。

**核心内容回顾**：
1.  **理解约束**：边缘设备在内存、算力上与云端存在巨大差距，内存层次结构是关键。
2.  **循环优化**：通过**重排**、**分块**、**展开**来优化缓存局部性和减少分支开销。
3.  **并行计算**：
    *   **SIMD**：利用向量指令一条指令处理多个数据。
    *   **多线程**：利用CPU多核（Pthread/OpenMP）。
    *   **CUDA**：利用GPU海量并行核心和Tensor Core。
4.  **推理优化**：
    *   **Im2Col**：将卷积转为矩阵乘。
    *   **原地计算**：减少深度卷积的内存占用。
    *   **内存布局**：根据卷积类型选择NHWC或NCHW。
    *   **Winograd**：用加法换乘法，加速小核卷积。

**实践应用**：结合这些技术，可以构建高效的推理引擎，例如**TinyEngine**。这使我们能够在笔记本电脑上本地部署量化后的大型语言模型（如LLaMA 2/3 7B/13B），实现离线对话功能。在接下来的实验（Lab 4 & 5）中，你们将实践AWQ量化和使用TinyEngine部署大模型。

![](img/6cdea097a850d3f9a9f2ad163674c9d7_276.png)

通过掌握这些底层优化技术，你将具备在从微控制器到服务器等各种设备上高效部署AI模型的能力。