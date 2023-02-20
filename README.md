# Data-structure-and-algorithm
数据结构与算法

# 排序

![image-20230220140533190](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230220140533190.png)

## 冒泡排序(Bubble Sort)

时间复杂度O(n^2)

需求:

​	排序前(4,5,6,3,2,1)

​	排序后(1,2,3,4,5,6)

排序原理:(每一次排序都会选出一个最大元素)

1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
2. 对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。
3. 针对所有的元素重复以上的步骤，除了最后一个。
4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230220094226773.png" alt="image-20230220094226773" style="zoom:50%;" />

代码实现(js):

```
<script>
    function BubbleSort(Array) {
      for (i = 0; i < Array.length; i++) {
        for (j = 0; j < Array.length - i - 1; j++) {
          if (Array[j] > Array[j + 1]) {
            let temp
            temp = Array[j]
            Array[j] = Array[j + 1]
            Array[j + 1] = temp
          }
        }
      }
      return Array
    }
    const arr = [4,5,6,3,2,1]
    console.log(arr)
    console.log(BubbleSort(arr))
  </script>
```

## 选择排序(Selection Sort)

时间复杂度O(n^2)

需求:

​	排序前:(4,6,8,7,9,2,10,1)

​	排序后:(1,2,4,6,7,8,9,10)

排序原理:

​	1.首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置.

​	2.再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序列的末尾

​	3.重复第二步，直到所有元素均排序完毕。

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230220132905153.png" alt="image-20230220132905153" style="zoom: 80%;" />

代码实现(js)

```
<script>
    //以升序为例
    function SelectionSort(Array) {
      let minIndex
      for (i = 0; i < Array.length - 1; i++) {
        let minIndex = i  //假定索引为i的是最小项
        for (j = i + 1; j < Array.length; j++) {
          if (Array[minIndex] > Array[j]) {
            minIndex = j //交换最小项的索引
          }
        }
        let temp
        temp = Array[i]
        Array[i] = Array[minIndex]
        Array[minIndex] = temp
      }
      return Array
    }
    let arr = [4,6,8,7,9,2,10,1]
    console.log(arr)
    console.log(SelectionSort(arr))
  </script>
```

## 插入排序(Insertion Sort)

时间复杂度O(n^2)

需求:

​	排序前:(4,3,2,10,12,1,5,6)

​	排序后:(1,2,3,4,5,6,10,12)

排序原理:

​	1.从第一个元素开始，该元素可以认为已经被排序；

​	2.取出下一个元素，在已经排序的元素序列中从后向前扫描；

​	3.如果该元素（已排序）大于新元素，将该元素移到下一位置；

​	4.重复步骤3，直到找到已排序的元素小于或者等于新元素的位置；

​	5.将新元素插入到该位置后；

​	6.重复步骤2~5。

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230220143555782.png" alt="image-20230220143555782" style="zoom:80%;" />

代码实现(js)

```
<script>
    function InsertionSort(arr) {
      for (i = 1; i < arr.length; i++) {
        let current = arr[i]
        let preIndex = i - 1
        while (preIndex >= 0 && arr[preIndex] > current) {
          arr[preIndex + 1] = arr[preIndex]
          preIndex--
        }
        arr[preIndex + 1] = current
      }
      return arr
    }
    let arr = [4, 3, 2, 10, 12, 1, 5, 6]
    console.log("排序前:", arr)
    console.log("排序后:", InsertionSort(arr))
  </script>
```

## 希尔排序(Shell Sort)

时间复杂度为O(n log n)

需求:

​	排序前:(9,1,2,5,7,4,8,6,3,5)

​	排序后:(1,2,3,4,5,5,6,7,8,9)

排序原理:

​	1.选定一个增长量h,按照增长量h作为数据分组的依据,对数据进行分组

​	2.对分好组的每一组数据完成插入排序

​	3.减小增长量,最小减为1,重复第二步操作

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230220145109192.png" alt="image-20230220145109192" style="zoom:80%;" />

***(上图的间隔h和代码所取间隔gap有区别(为了更好理解希尔排序原理),实际间隔取值情况及排序见下图)***

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230220153628323.png" alt="image-20230220153628323" style="zoom: 67%;" />

代码实现(js):

```
<script>
    function ShellSort(arr) {
      var len = arr.length,
        temp,
        gap = 1;
      while (gap < len / 3) {          //动态定义间隔序列
        gap = gap * 3 + 1;
      }
      for (gap; gap > 0; gap = Math.floor(gap / 3)) {
        //console.log("间隔gap", gap)
        for (var i = gap; i < len; i++) {
          temp = arr[i];
          for (var j = i - gap; j >= 0 && arr[j] > temp; j = j - gap) {
            arr[j + gap] = arr[j];
          }
          arr[j + gap] = temp;
          //console.log(arr)
        }

      }
      return arr;
    }
    let arr = [9, 1, 2, 5, 7, 4, 8, 6, 3, 5]
    console.log("排序前:", arr)
    console.log("排序后:", ShellSort(arr))
  </script>
```

## 归并排序(Merge Sort)

时间复杂度为O(n log n)

需求:

​	排序前:(8,4,5,7,1,3,6,2)

​	排序后:(1,2,3,4,5,6,7,8)

排序原理:

​	1.把长度为n的输入序列分成两个长度为n/2的子序列；

​	2.对这两个子序列分别采用归并排序；

​	3.将两个排序好的子序列合并成一个最终的排序序列。

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230220181335160.png" alt="image-20230220181335160" style="zoom:80%;" />

代码实现(js)

```
<script>
    function MergeSort(arr) {  //采用自上而下的递归方法
      var len = arr.length;
      if (len < 2) {
        return arr;
      }
      var middle = Math.floor(len / 2),
        left = arr.slice(0, middle),
        right = arr.slice(middle);
      return merge(MergeSort(left), MergeSort(right));
    }

    function merge(left, right) {
      var result = [];

      while (left.length && right.length) {
        //每次将小的推入result中
        if (left[0] <= right[0]) {
          result.push(left.shift());
        } else {
          result.push(right.shift());
        }
      }
      while (left.length)
        result.push(left.shift());

      while (right.length)
        result.push(right.shift());

      return result;
    }
    let arr = [8, 4, 5, 7, 1, 3, 6, 2]
    console.log("排序前:", arr)
    console.log("排序后:", MergeSort(arr))
  </script>
```



# 线性表(List)

线性表是n个具有相同特性的元素的有限序列

分为顺序表和链表
