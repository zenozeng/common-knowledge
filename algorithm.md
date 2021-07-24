# Algorithm

## Sorting

- 基于比较的排序（非并行情况下）：下界为 `O(nlogn)`

https://zh.wikipedia.org/wiki/排序算法

### 冒泡排序

> - 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
> - 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
> - 针对所有的元素重复以上的步骤，除了最后一个。
> - 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

```javascript
Array.prototype.bubble_sort = function() {
	var i, j, temp;
	for (i = 0; i < this.length - 1; i++)
		for (j = 0; j < this.length - 1 - i; j++)
			if (this[j] > this[j + 1]) {
				temp = this[j];
				this[j] = this[j + 1];
				this[j + 1] = temp;
			}
	return this;
};
```

- https://zh.wikipedia.org/wiki/冒泡排序
- https://visualgo.net/zh/sorting

### 选择排序

> 从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾

- https://zh.wikipedia.org/wiki/选择排序
- https://visualgo.net/zh/sorting

### 插入排序

### 归并排序

### 快排
