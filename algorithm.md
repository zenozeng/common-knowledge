# Algorithm

## Sorting

- 基于比较的排序（非并行情况下）：下界为 `O(nlogn)`

https://zh.wikipedia.org/wiki/排序算法

### 冒泡排序

> - 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
> - 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
> - 针对所有的元素重复以上的步骤，除了最后一个。
> - 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

- https://zh.wikipedia.org/wiki/冒泡排序
- https://visualgo.net/zh/sorting

### 选择排序

> 从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾

- https://zh.wikipedia.org/wiki/选择排序
- https://visualgo.net/zh/sorting

### 插入排序

> 和打扑克牌时，从牌桌上逐一拿起扑克牌，在手上排序的过程类似

持续从未排序元素中选择首个，放到已排序序列之中并保持顺序

- https://zh.wikipedia.org/wiki/插入排序
- https://visualgo.net/zh/sorting

### 归并排序

> - 分割：递归地把当前序列平均分割成两半。
> - 集成：在保持元素顺序的同时将上一步得到的子序列集成到一起（归并）。

- 分治
- https://zh.wikipedia.org/wiki/归并排序
- https://visualgo.net/zh/sorting

### 快排

平均 O(nlogn)，最坏 O(n<sup>2</sup>)

> - 挑选基准值：从数列中挑出一个元素，称为“基准”（pivot），
> - 分割：重新排序数列，所有比基准值小的元素摆放在基准前面，所有比基准值大的元素摆在基准后面（与基准值相等的数可以到任何一边）。在这个分割结束之后，对基准值的排序就已经完成，
> - 递归排序子序列：递归地将小于基准值元素的子序列和大于基准值元素的子序列排序。

- https://zh.wikipedia.org/wiki/快速排序
- https://visualgo.net/zh/sorting
