# GC

## V8

### Generations

#### Young Generation

- Nursery: 新对象分配到这里
- Intermediate: 经过 1 次 GC

#### Old Generation

Intermediate 里再经过一次 GC

### Major GC (Full Mark-Compact)

对整个 Heap 的 GC

- Marking
- Sweeping
- Compaction 为避免对 long-living 对象的大量拷贝，只有高度碎片化的页会发生 Compaction

### 

## References

https://v8.dev/blog/trash-talk
