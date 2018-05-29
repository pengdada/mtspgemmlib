Sparse General Matrix-Matrix Multiplication for multi-core CPU and Intel KNL
======

# Versions
1.0 (May, 2018)


# Introduction
Sparse matrix computation is a key kernel of many applications. This library provides fast sparse general vmatrix-matrix multiplication (SpGEMM) kernels for multi-core CPU and Intel KNL. More information can be found in (1).

(1) Yusuke Nagasaka, Satoshi Matsuoka, Ariful Azad, Aydin Buluc, "High-performance sparse matrix-matrix products on Intel KNL and multicore architectures", https://arxiv.org/abs/1804.01698


# Requirement
Intel Compiler 18.0.1


# Preparation
To use this library, the first thing you need to do is to modify the Makefile with correct path to Intel Compiler.


# Run sample program
The sample program executes C=AB, where A, B and C are sparse matrice. We provide three sample programs, and they executes SpGEMM in different way, MKL-SpGEMM, Heap-SpGEMM and Hash-SpGEMM.

(0-a) compile for multi-core CPU
```
make sample_hw
```

(0-b) compile for KNL
```
make sample_knl
```

(1) run Heap-SpGEMM for multi-core CPU on synthetic Erdos-Renyi matrices with scale=10, edgefactor=4
```
./bin/HeapSpGEMM_hw gen er 10 4
```

(2) run Hash-SpGEMM for KNL on synthetic Graph500 matrices with scale=10, edgefactor=16
```
./bin/HashSpGEMM_knl gen rmat 10 16
```

(3) run MKL-SpGEMM for multi-core CPU on matrices in matrix market format
```
./bin/MKLSpGEMM_hw text (path to the file of matrix A) (path to the file of matrix B)
```


# How to use in your program
Copy all of header files (*.h) in this directory to your program. To use the library, include files in your code. Below is an example.
```
#include "utility.h"
#include "CSC.h"
#include "CSR.h"
#include "multiply.h"
#include "heap_mult.h"
#include "hash_mult.h" // for KNL
//#include "hash_mult_hw.h" // for multi-core CPU
```



