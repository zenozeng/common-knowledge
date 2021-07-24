# DS

## Tree

### B+ Tree

#### InnoDB B+ Tree Index

可以参考 Jeremy Cole 绘制的这张图：

![](B_Tree_Structure.png)

- Value 都在叶子结点，内存可以塞下更多的 Keys
- 同层的 Pages 都 doubly-linked
- Height
- 适合范围查询

https://blog.jcole.us/2013/01/10/btree-index-structures-in-innodb/

### LSM Tree (Log-structured Merge-tree)

经常搭配 Bloom Filter 和 SSTable。

- https://www.cs.umb.edu/~poneil/lsmtree.pdf
- 随机 IO -> 顺序 IO
- RocksDB, HBase
- https://leonlibraries.github.io/2017/05/18/从LSM到HBase/

## Bloom Filter

> - "possibly in set" or "definitely not in set"
> - To add an element, feed it to each of the k hash functions to get k array positions. Set the bits at all these positions to 1.
> - To query for an element (test whether it is in the set), feed it to each of the k hash functions to get k array positions. If any of the bits at these positions is 0, the element is definitely not in the set; if it were, then all the bits would have been set to 1 when it was inserted. If all are 1, then either the element is in the set, or the bits have by chance been set to 1 during the insertion of other elements, resulting in a false positive.

- https://en.wikipedia.org/wiki/Bloom_filter
- https://leveldb-handbook.readthedocs.io/zh/latest/bloomfilter.html
- [Bloom Filters - the math](https://web.archive.org/web/20210301224639/http://pages.cs.wisc.edu/~cao/papers/summary-cache/node8.html)
- m bits, n elements, m/n=10, k=7, rate=0.00819
