# 数据结构与算法

## 排序算法

- 快速排序

快速排序是由东尼·霍尔发展的一种排序算法。时间复杂度为O(N*logN)

在平均状况下，排序 n 个项目要Ο(n log n)次比较。在最坏状况下则需要Ο(n2)次比较，但这种状况并不常见。事实上，快速排序通常明显比其他Ο(n log n) 算法更快，因为它的内部循环可以在大部分的架构上，很有效率地被实现出来。

主要采用了递归和分治的思想。选择标尺后，进行遍历数组，将大于标尺的放到一个数组，将小于标尺的放置到一个数组。再递归调用本函数并记录结果。

具体步骤：

- 从数列中挑出一个数作为基准元素。通常选择第一个或最后一个元素。
- 扫描数列，以基准元素为比较对象，把数列分成两个区。规则是：小的移动到基准元素前面，大的移到后面，相等的前后都可以。分区完成之后，基准元素就处于数列的中间位置。
- 然后再用同样的方法，递归地排序划分的两部分。
- 递归的结束条件是数列的大小是0或1，也就是永远都已经被排序好了

```php
function quickSort($arr)
{
    //先判断是否需要继续进行
    $length = count($arr);
    if($length <= 1) {
        return $arr;
    }
    //选择一个标尺,通常选择第一个元素
    $base_num = $arr[0];
    //初始化
    $left = array();//小于标尺的
    $right = array();//大于标尺的
    for($i=1;$i<$length;$i++) {
        if($base_num > $arr[$i]) {
            $left[] = $arr[$i];
        }else {
            $right[] = $arr[$i];
        }
    }
    //递归调用并记录
    $left = $this->quickSort($left);
    $right = $this->quickSort($right);
    //合并
    return array_merge($left,array($base_num), $right);
}
```

- 冒泡排序

冒泡排序是一种简单的排序算法。

算法重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作重复地进行，直到没有再需要交换，也就是说该数列已经排序完成。因为排序过程让较大的数往下沉，较小的往上冒，故而叫冒泡法

具体步骤

- 从第一个元素开始，比较相邻的元素，如果第一个比第二个大，就交换他们两个。
- 从开始第一对到结尾的最后一对，对每一对相邻元素作同样的工作。比较结束后，最后的元素应该会是最大的数。
- 对所有的元素重复以上的步骤，除了最后一个。
- 重复上面的步骤，每次比较的对数会越来越少，直到没有任何一对数字需要比较。

```php
function bubbleSort($arr)
{
    $len = count($arr);
    for($i = 1; $i < $len; $i++) {
        for($k = 0; $k < $len - $i; $k++) {
            if($arr[$k] > $arr[$k + 1]) {
                $tmp = $arr[$k + 1];
                $arr[$k + 1] = $arr[$k];
                $arr[$k] = $tmp;
            }
        }
    }

    return $arr;
}
```

- 插入排序

插入排序是一种简单直观的排序算法。

插入排序的工作原理是：将需要排序的数，与前面已经排好序的数据从后往前进行比较，使其插入到相应的位置。

插入排序在实现上，通常采用in-place排序，即只需用到O(1)的额外空间的排序。

因而，在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。

具体步骤

- 从第一个元素开始，该元素可以认为已经被排序；
- 取出下一个元素，在已经排序的元素序列中从后向前扫描；
- 如果以排序的元素大于新元素，将该元素移到下一位置；
- 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置；
- 将新元素插入到该位置中；
- 重复步骤2

```php
function insertSort($arr)
{
    $len = count($arr);

    for ($i = 1; $i < $len; $i++) {
        $tmp = $arr[$i];
        for ($j = $i - 1; $j >= 0; $j--) {
            if ($tmp < $arr[$j]) {
                $arr[$j + 1] = $arr[$j];
                $arr[$j] = $tmp;
            } else {
                break;
            }
        }
    }

    return $arr;
}
```

- 选择排序

选择排序是一种简单直观的排序算法。

具体步骤

- 首先，在序列中找到最小元素，存放到排序序列的起始位置；
- 接着，从剩余未排序元素中继续寻找最小元素，放到已排序序列的末尾。
- 重复第二步，直到所有元素均排序完毕。

```php
function selectSort($arr)
{
    $len = count($arr);

    for ($i = 0; $i < $len; $i++) {
        $p = $i;

        for ($j = $i + 1; $j < $len; $j++) {
            if ($arr[$p] > $arr[$j]) {
                $p = $j;
            }
        }

        $tmp = $arr[$p];
        $arr[$p] = $arr[$i];
        $arr[$i] = $tmp;
    }

    return $arr;
}
```

- 归并排序

归并排序是建立在归并操作上的一种有效的排序算法。时间复杂度为O(N*logN)

归并排序将待排序的序列分成若干组，保证每组都有序，然后再进行合并排序，最终使整个序列有序。

该算法是采用分治法的一个非常典型的应用。

算法步骤：

- 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列；
- 设定两个指针，最初位置分别为两个已经排序序列的起始位置
- 比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置
- 重复步骤3直到某一指针达到序列尾
- 将另一序列剩下的所有元素直接复制到合并序列尾

```php
function merge_sort(array $lists)
{
    $n = count($lists);
    if ($n <= 1) {
        return $lists;
    }
    $left = merge_sort(array_slice($lists, 0, floor($n / 2)));
    $right = merge_sort(array_slice($lists, floor($n / 2)));
    $lists = merge($left, $right);
    return $lists;
}

function merge(array $left, array $right)
{
    $lists = [];
    $i = $j = 0;
    while ($i < count($left) && $j < count($right)) {
        if ($left[$i] < $right[$j]) {
            $lists[] = $left[$i];
            $i++;
        } else {
            $lists[] = $right[$j];
            $j++;
        }
    }
    $lists = array_merge($lists, array_slice($left, $i));
    $lists = array_merge($lists, array_slice($right, $j));
    return $lists;
}
```

- 堆排序

