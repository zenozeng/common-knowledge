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

### Minor GC (Scavenger)

对新生代进行 GC

V8 采用 `semi-space` 设计。一半空，作为 `To-Space`，从 `From-Space` 拷贝对象过去。

### State of GC in V8 (2019)

- parallel scavenging
- concurrent marking
- concurrent sweeping
- parallel compaction

## References

https://v8.dev/blog/trash-talk
