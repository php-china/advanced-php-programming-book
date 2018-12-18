# 数据结构与算法

## 查找算法

- 二分查找

```php
// 迭代
function dichotomyIterationSearch($arr, $n, $v)
{
    $left   = 0;
    $right  = $n - 1;
    while ($left <= $right) {
        $middle  = bcdiv(bcadd($right, $left), 2);
        if ($arr[$middle] > $v) {
            $right = $middle - 1;
        } elseif ($arr[$middle] < $v) {
            $left  = $middle + 1;
        } else {
            return $middle;
        }
    }
    return -1;
}
// 递归

function dichotomyRecursionSearch($arr, $low, $high, $v)
{
    $middle = bcdiv(bcadd($low, $high), 2);
 
    if ($low < $high) {
        if ($arr[$middle] > $v) {
            $high = $middle - 1;
            return dichotomyRecursionSearch($arr, $low, $high, $v);
        } elseif ($arr[$middle] < $v) {
            $low = $middle + 1;
            return dichotomyRecursionSearch($arr, $low, $high, $v);
        } else {
            return $middle;
        }
    } elseif ($high == $low) {
        if ($arr[$middle] == $v) {
            return $middle;
        } else {
            return -1;
        }
    }
    return -1;
}
```