# MinIO

MinIO 是一套开源的分布式对象存储方案，设计成无需 rebalancing，这一点显著得简化了系统架构。
同时 Erasure Coding 的设计也比 Replication 更经济。
本文会概要描述一下 MinIO 的核心概念以及故障容忍计算。

## Core Concepts

### Volume

一个卷，可以是一个本地目录（通常每个 volume mount 各自的磁盘），在 Kubernetes 下是一个 PV。

### Erasure Coding

MinIO 的核心。可以仔细阅读：https://docs.min.io/minio/baremetal/concepts/erasure-coding.html

Erasure Coding 将每个文件对象拆分为 K 个 data blocks 和 N 个 parity blocks，parity blockss 被用于 data blocks 丢失或损毁的时候重新构建。

现在假设每个文件对象被拆分为 K + N = 16 个 blocks：

如果 Erasure Coding 设置为 EC:4（MinIO 默认值，每个 Object 有 4 个 parity blocks），则：
- 文件对象会被拆分为 K=12 个 data blocks 和 N=4 个 parity blocks
- Storage Ratio 为 0.75（1PB 物理容量产生 0.75 PB 可用容量）
- 允许在 4 个 blocks offline 的时候进行读操作
- 允许在 4 个 blocks offline 的时候进行写操作

如果 Erasure Coding 设置为 EC:8（每个 Object 有 8 个 parity blocks） ，则：
- 文件对象会被拆分为 K=8 个 data blocks 和 N=8 个 parity blocks
- Storage Ratio 为 0.5
- 允许在 8 个 blocks offline 的时候进行读操作
- 允许在 7 个 blocks offline 的时候进行写操作（8个的话刚好是16的一半，因此写操作需要 9 个 volumes online 来避免脑裂问题）

### Erasure Set

## Erasure Code 计算

https://min.io/product/erasure-code-calculator

## References

- https://docs.min.io/minio/k8s/core-concepts/core-concepts.html
- https://docs.min.io/minio/baremetal/concepts/erasure-coding.html
- https://blog.min.io/no-rebalancing-object-storage/