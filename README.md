# Data-structure-and-algorithm
***看看就好,别当真***

数据结构与算法

[TOC]



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

## 快速排序(Quick Sort)

时间复杂度为O(n log n)

需求:

​	排序前:(6,1,2,7,9,3,4,5,8)

​	排序后:(1,2,3,4,5,6,7,8,9)

排序原理:

​	1.首先设定一个分界值,通过该分界值将数组分成左右两部分

​	2.将大于或等于该分界值的元素放到数组右边,小于该分界值的的元素放到数组左		边;此时分界值左边的元素都小于该分界值的,分界值右边的元素都小于或等于		该分界值

​	3.然后,左边和右边的数组数据又可以独立排序,对左边的数组数据又可以取一个		分界值将数据分成两部分,分界值左边存放较小值,分界值右边存放较大值;对右		侧的数组数据同样如此操作

​	4.重复上述过程,可以看出这是一个递归过程,通过递归将左侧数据拍好后在递归		排好右侧数据,当左右两侧数据都排好后,整个数组数据就排序完成了

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230221101251656.png" alt="image-20230221101251656" style="zoom:80%;" />

代码实现(js):

```
 <script>
    //arr为要排序的数组,start为需要排序的起始位置索引,end为要排序的结束位置索引
    function QuickSort(arr, start, end) {
      var len = arr.length,
        partitionIndex,
        start = typeof start != 'number' ? 0 : start,
        end = typeof end != 'number' ? len - 1 : end;

      if (start < end) {
        partitionIndex = partition(arr, start, end);
        QuickSort(arr, start, partitionIndex - 1);
        QuickSort(arr, partitionIndex + 1, end);
      }
      return arr;
    }

    function partition(arr, start, end) {     //分区操作
      var pivot = start//设定基准值（pivot）
      index = pivot + 1
      for (var i = index; i <= end; i++) {
        if (arr[i] < arr[pivot]) {
          swap(arr, i, index);
          index++;
        }
      }
      swap(arr, pivot, index - 1);
      return index - 1;
    }

    function swap(arr, i, j) {
      var temp = arr[i];
      arr[i] = arr[j];
      arr[j] = temp;
    }
    let arr = [6, 1, 2, 7, 9, 3, 4, 5, 8]
    console.log("排序前:", arr)
    console.log("排序后:", QuickSort(arr))
  </script>
```

## 堆排序(Heap Sort)

代码实现(js)

```
<script>
    var len;    //因为声明的多个函数都需要数据长度，所以把len设置成为全局变量
    function buildMaxHeap(arr) {   //建立大顶堆
      len = arr.length;
      for (var i = Math.floor(len / 2); i >= 0; i--) {
        heapify(arr, i);
      }
    }

    function heapify(arr, i) {     //堆调整
      var left = 2 * i + 1,
        right = 2 * i + 2,
        largest = i;

      if (left < len && arr[left] > arr[largest]) {
        largest = left;
      }

      if (right < len && arr[right] > arr[largest]) {
        largest = right;
      }

      if (largest != i) {
        swap(arr, i, largest);
        heapify(arr, largest);
      }
    }

    function swap(arr, i, j) {
      var temp = arr[i];
      arr[i] = arr[j];
      arr[j] = temp;
    }

    function HeapSort(arr) {
      buildMaxHeap(arr);

      for (var i = arr.length - 1; i > 0; i--) {
        swap(arr, 0, i);
        len--;
        heapify(arr, 0);
      }
      return arr;
    }
    let arr = [91, 69, 96, 13, 35, 65, 46, 65, 10, 30, 20]
    console.log("排序前:", arr)
    console.log("排序后:", HeapSort(arr))
  </script>
```



# 线性表(List)

线性表是n个具有相同特性的元素的有限序列

## 链表(LinkedList)

链表不同于数组,链表中的元素在内存中不是连续放置的,每个元素由一个存储该元素本身的节点和一个指向下一个元素的引用(指针)组成;如下图

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230223145822953.png" alt="image-20230223145822953" style="zoom:80%;" />

链表的好处在于我们在添加和删除元素是不需要移动其他元素;但是链表需要使用指针,即我们可以使用指针访问链表任意元素,但若想访问链表中间的元素则需要从头开始遍历每一个元素直到遍历到所查找的元素

**js创建链表及其方法代码:**

//push(element):向链表尾部添加一个新元素

//insert(element,position):向链表特定位置插入一个新元素

//getElementAt(position):返回链表中特定位置的元素,如果不存在该元素则返回undefined

//remove(element):从链表中移除一个元素

//indexOf(element):返回元素在链表中的索引,如果链表中没有该元素则返回-1

//removeAt(position):移除链表中特定位置的元素,并将其返回

//isEmpty():如果链表不包含任何元素返回true;如果链表长度大于0返回false

//size():返回链表中的元素个数

//toString():返回整个链表的字符串

```
<script>
    function defaultEquals(a, b) {
      return a === b
    }
    class LinkedList {
      constructor(equalsFn = defaultEquals) {
        this.count = 0
        this.head = undefined
        this.equalsFn = equalsFn
      }
      //比较链表中的元素是否相等
      equalsFn(a, b) {
        return a === b
      }
      //push(element):向链表尾部添加一个新元素
      push(element) {
        const node = new Node(element)
        let current
        if (this.head == null) {
          this.head = node
        } else {
          current = this.head
          while (current.next != null) {
            current = current.next
          }
          current.next = node
        }
        this.count++
      }
      //insert(element,position):向链表特定位置插入一个新元素
      insert(element, position) {
        if (position >= 0 && position < this.count) {
          const node = new Node(element)
          if (position === 0) {
            const current = this.head
            node.next = current
            this.head = node
          } else {
            const previous = this.getElementAt(position - 1)
            const current = previous.next
            node.next = current
            previous.next = node
          }
          this.count++
          return true
        }
        return false
      }
      //getElementAt(position):返回链表中特定位置的元素,如果不存在该元素则返回undefined
      getElementAt(position) {
        if (position >= 0 && position < this.count) {
          let node = this.head
          for (let i = 0; i < position && node != null; i++) {
            node = node.next
          }
          return node
        }
        return undefined
      }
      //remove(element):从链表中移除一个元素
      remove(element) {
        const position = this.indexOf(element)
        return this.removeAt(position)
      }
      //indexOf(element):返回元素在链表中的索引,如果链表中没有该元素则返回-1
      indexOf(element) {
        let current = this.head
        for (let i = 0; i < this.count && current != null; i++) {
          if (this.equalsFn(element, current.element)) {
            return i
          }
          current = current.next
        }
        return -1
      }
      //removeAt(position):移除链表中特定位置的元素,并将其返回
      removeAt(position) {
        if (position >= 0 && position < this.count) {
          let current = this.head
          if (position === 0) {
            this.head = current.next
          } else {
            let previous = this.getElementAt(position - 1)
            current = previous.next
            previous.next = current.next
          }
          this.count--
          return current.element
        }
        return undefined
      }
      //isEmpty():如果链表不包含任何元素返回true;如果链表长度大于0返回false
      isEmpty() {
        return this.size() === 0
      }
      //size():返回链表中的元素个数
      size() {
        return this.count
      }
      //toString():返回整个链表的字符串
      toString() {
        if (this.head == null) {
          return ''
        }
        let objString = `${this.head.element}`
        let current = this.head.next
        for (let i = 0; i < this.count && current != null; i++) {
          objString = `${objString},${current.element}`
          current = current.next
        }
        return objString
      }
    }
    class Node {
      constructor(element) {
        this.element = element
        this.next = undefined
      }
    }
    const list = new LinkedList()
    console.log(list.isEmpty())//true
    list.push(15)
    list.push(10)
    console.log(list.toString())//15,10
    list.insert(20, 1)
    console.log(list.toString())//15,20,10
    list.remove(10)
    console.log(list.toString())//15,20
    list.push(25)
    list.insert(99, 2)
    console.log(list.size())//4
    console.log(list.toString())//15,20,99,25
  </script>
```

## 双向链表(DoublyLinkedList)

在链表中,一个节点只有链向下一个节点的链接;在双向链表中,链接是双向的,一个链向下一元素,另一个链向前一个元素

代码实现

```
class DoublyNode extends Node {
      constructor(element, next, prev) {
        super(element, next)
        this.prev = prev
      }
    }
    class DoublyLinkedList extends LinkedList {
      constructor(equalsFn = defaultEquals) {
        super(equalsFn)
        this.tail = undefined
      }
      insert(element, position) {
        if (position >= 0 && position < this.count) {
          const node = new DoublyNode(element)
          let current = this.head
          if (position === 0) {
            if (this.head == null) {
              this.head = node
              this.tail = node
            } else {
              node.next = this.head
              current.prev = node
              this.head = node
            }
          } else if (position === this.count) {
            current = this.tail
            current.next = node
            node.prev = current
            this.tail = node
          } else {
            const previous = this.getElementAt(position - 1)
            current = previous.next
            node.next = current
            previous.next = node
            current.prev = node
            node.prev = previous
          }
          this.count++
          return true
        }
        return false
      }
      removeAt(position) {
        if (position >= 0 && position < this.count) {
          let current = this.head
          if (position === 0) {
            this.head = current.next
            if (this.count === 1) {
              this.tail = undefined
            } else {
              this.head.prev = undefined
            }
          } else if (position === this.count - 1) {
            current = this.tail
            this.tail = current.prev
            this.tail.next = undefined
          } else {
            let current = this.getElementAt(position)
            const previous = current.prev
            previous.next = current.next
            current.next.prev = previous
          }
          this.count--
          return current.element
        }
        return undefined
      }
    }
    const doublylist = new DoublyLinkedList()
    console.log(doublylist.isEmpty())//true
    doublylist.push(15)
    doublylist.push(10)
    console.log(doublylist.toString())//15,10
    doublylist.insert(20, 1)
    console.log(doublylist.toString())//15,20,10
    doublylist.removeAt(0)//此处有个小bug,删除最后一个元素时会报错,目前还未找到原因
    console.log(doublylist.toString())//15,20
    doublylist.push(25)
    doublylist.insert(99, 2)
    console.log(doublylist.size())//4
    console.log(doublylist.toString())//15,20,99,25
```

## 循环链表(CircularLinkedList)

循环链表可以像链表一样只有单向引用;也可以向双向链表一样有双向引用;

循环链表和链表的区别在于它最后一个元素指向下一个元素的指针(tail.next)不是引用undefined,而是指向第一个元素head

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230224101119483.png" alt="image-20230224101119483" style="zoom:80%;" />

双向循环链表有指向head元素的tail.next和指向tail元素的head.prev

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230224101311757.png" alt="image-20230224101311757" style="zoom:80%;" />

代码实现:(**补充说明:下列重写方法只是测试需要写了部分,并未将链表的方法全部重写,可按自己需求进行重写**)

```
class CircularLinkedList extends LinkedList {
      constructor(equalsFn = defaultEquals) {
        super(equalsFn)
      }
      //重写toString方法
      toString() {
        if (this.head == null) {
          return ''
        }
        let objString = `${this.head.element}`
        let current = this.head.next
        for (let i = 0; i < this.count - 1 && current != null; i++) {
          objString = `${objString},${current.element}`
          current = current.next
        }
        return objString
      }
      //重写push方法
      push(element) {
        const node = new Node(element)
        let current
        if (this.head == null) {
          this.head = node
          node.next = this.head
        } else {
          current = this.head
          node.next = this.head
          current = this.getElementAt(this.count - 1)
          current.next = node
        }
        this.count++
      }
      //重写insert方法
      insert(element, position) {
        if (position >= 0 && position < this.count) {
          const node = new Node(element)
          let current = this.head
          if (position === 0) {
            if (this.count == null) {
              this.head = node
              node.next = this.head
            } else {
              node.next = this.head
              current = this.getElementAt(this.count - 1)
              current.next = node
              this.head = node
            }
          } else {
            const previous = this.getElementAt(position - 1)
            node.next = previous.next
            previous.next = node
          }
          this.count++
          return true
        }
        return false
      }
      //重写removeAt方法
      removeAt(position) {
        if (position >= 0 && position < this.count) {
          let current = this.head
          if (position === 0) {
            if (this.count === 1) {
              this.head = undefined
            } else {
              let removed = this.head
              current = this.getElementAt(this.count - 1)
              //console.log(current)
              this.head = this.head.next
              current.next = this.head
              current = removed
            }
          } else {
            const previous = this.getElementAt(position - 1)
            current = previous.next
            previous.next = current.next
          }
          this.count--
          return current.element
        }
        return undefined
      }
    }
    const circularlist = new CircularLinkedList()
    console.log(circularlist.isEmpty())//true
    circularlist.push(15)
    circularlist.push(10)
    console.log(circularlist.toString())//15,10
    circularlist.insert(20, 0)
    console.log(circularlist.toString())//20,15,10
    circularlist.removeAt(0)
    console.log(circularlist.toString())//15,10
    circularlist.push(25)
    circularlist.insert(99, 1)
    console.log(circularlist.size())//4
    console.log(circularlist.toString())//15,99,10,25
```



# 栈(Stack)

栈是一种遵循***后进先出(LIFO)***原则的有序集合,在栈里新元素都靠近栈顶,旧元素都靠近栈底.

在js中可以创建一个类来表示栈,并利用数组来保存栈中的元素,并使用

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230221163048205.png" alt="image-20230221163048205" style="zoom:80%;" />

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230221163119189.png" alt="image-20230221163119189" style="zoom:80%;" />

代码实现(**创建一个基于数组的栈**):

```
<script>
    //创建一个类来表示栈
    class Stack {
      constructor() {
        this.items = [];//利用数组来保存栈里的元素
      }
      //push(element(s)): 添加一个(或儿个)新元素到栈顶
      push(element) {
        this.items.push(element);
      };
      //pop(): 移除栈顶的元素，同时返回被移除的元素
      pop() {
        return this.items.pop();
      };
      //peek(): 返回栈顶的元素, 不对栈做任何修改(该方法不会移除栈顶的元素, 仅仅返回它)
      peek() {
        return this.items[this.items.length - 1]
      };
      //isEmpty(): 如果栈里没有任何元素就返回true.否则返回false
      isEmpty() {
        return this.items.length === 0
      };
      //clear(): 移除栈里的所有元素
      clear() {
        this.items = []
      };
      //size(): 返回栈里的元素个数。该方法和数组的length属性很类似
      size() {
        return this.items.length
      };
    }
    //使用stack
    const stack = new Stack()
    console.log(stack.isEmpty())//true
    stack.push(5)
    stack.push(8)
    console.log(stack.peek())//8
    stack.push(11)
    stack.push(15)
    stack.pop()
    stack.pop()
    console.log(stack.size())//2

  </script>
```

在js中我们也可以通过js对象来存储所有栈元素并遵循LIFO原则

代码实现(**js基于对象实现栈**):

```
<script>
    //创建一个基于object的栈,并用count属性来记录栈的大小
    class Stack {
      constructor() {
        this.count = 0;
        this.items = {};
      }
      push(element) {
        this.items[this.count] = element
        this.count++
      }
      pop() {
        if (this.isEmpty()) {
          return undefined
        }
        this.count--
        let result = this.items[this.count]
        delete this.items[this.count]
        return result;
      };
      peek() {
        if (this.isEmpty()) {
          return undefined
        }
        return this.items[this.count - 1]
      };
      isEmpty() {
        return this.count === 0
      };
      clear() {
        this.count = 0
        this.items = {}
      };
      size() {
        return this.count
      };
      //打印栈中所有元素
      toString() {
        if (this.isEmpty()) {
          return ''
        }
        let objString = `${this.items[0]}`
        for (let i = 1; i < this.count; i++) {
          objString = `${objString},${this.items[i]}`
        }
        return objString
      }
    }
    const stack = new Stack()
    console.log(stack.isEmpty())//true
    stack.push(5)
    stack.push(8)
    console.log(stack.peek())//8
    stack.push(11)
    stack.push(15)
    stack.pop()
    stack.pop()
    console.log(stack.size())//2
    console.log(stack.toString())//5,8
  </script>
```

***案例(十进制转化为二进制)***

```
<script>
    //创建一个基于object的栈,并用count属性来记录栈的大小
    class Stack {
      constructor() {
        this.count = 0;
        this.items = {};
      }
      push(element) {
        this.items[this.count] = element
        this.count++
      }
      pop() {
        if (this.isEmpty()) {
          return undefined
        }
        this.count--
        let result = this.items[this.count]
        delete this.items[this.count]
        return result;
      };
      peek() {
        if (this.isEmpty()) {
          return undefined
        }
        return this.items[this.count - 1]
      };
      isEmpty() {
        return this.count === 0
      };
      clear() {
        this.count = 0
        this.items = {}
      };
      size() {
        return this.count
      };
      //打印栈中所有元素
      toString() {
        if (this.isEmpty()) {
          return ''
        }
        let objString = `${this.items[0]}`
        for (let i = 1; i < this.count; i++) {
          objString = `${objString},${this.items[i]}`
        }
        return objString
      }
    }
    //十进制转化为二进制
    function decimalToBinary(decNumber) {
      const remStack = new Stack();
      let number = decNumber;
      let rem;
      let binaryString = '';
      while (number > 0) {
        rem = Math.floor(number % 2);
        remStack.push(rem);
        number = Math.floor(number / 2);
        while (!remStack.isEmpty()) {
          binaryString = remStack.pop().toString() + binaryString;
        }
      }
      return binaryString;
    }
    console.log(decimalToBinary(233))//11101001
    //console.log(decimalToBinary(10))
    //console.log(decimalToBinary(1000))
  </script>
```

***案例(有效的括号)***

Stack使用之前js创建的类(此处省略)

```
function isVaild(s) {
      //需要先校验s格式
      let pattern = /^(\(|\)|\[|\]|\{|\})*$/
      if (!pattern.test(s)) {
        return undefined
      }
      const stack = new Stack()
      let vaild = true
      let str = s.split(" ").join('')

      for (let i = 0; i < str.length; i++) {
        if (str[i] == '(' || str[i] == '[' || str[i] == '{') {
          stack.push(str[i])
        } else if (str[i] == ')' && stack.size() !== 0 && stack.peek() == '(') {
          stack.pop()
        } else if (str[i] == ']' && stack.size() !== 0 && stack.peek() == '[') {
          stack.pop()
        } else if (str[i] == '}' && stack.size() !== 0 && stack.peek() == '{') {
          stack.pop()
        } else {
          vaild = false
          break
        }
      }
      if (stack.size() == 0 && vaild == true) {
        return true
      } else {
        return false
      }
    }
    console.log('(()):', isVaild('(())'))
    console.log('({]:', isVaild('({]'))
    console.log('{[]):', isVaild('{[])'))
    console.log('(){}[]:', isVaild('(){}[]'))
    console.log('({[:', isVaild('({['))
    console.log('(a)', isVaild('(a)'))
```

***案例(汉诺塔)***

```
function towerOfHanoi(plates, source, helper, dest, sourceName, helperName, destName, moves = []) {
      console.log(moves.length)
      //如果盘子的数字不大于0 ，那么直接返回moves,终止递归的条件。
      if (plates <= 0) return moves;

      if (plates === 1) {
        dest.push(source.pop());
        const move = {};
        move[sourceName] = source.toString();
        move[helperName] = helper.toString();
        move[destName] = dest.toString();
        moves.push(move);
      } else {
        /*递归调用自身。并且将盘子的数量减少一个，这里交换了dest和helper的位置，是为了dest.push中存入的栈是helper栈，
        也就是说是为了存入对应的柱子*/
        towerOfHanoi(plates - 1, source, dest, helper, sourceName, destName, helperName, moves);
        //从源柱子拿出最顶层的一个放入目标柱子（如果dest和helper互换了位置，那么其实这里的dest实际上代表的是helper）
        dest.push(source.pop());
        //声明常量，用来存储当前各个柱子的盘子栈况
        const move = {};
        move[sourceName] = source.toString();
        move[helperName] = helper.toString();
        move[destName] = dest.toString();
        // 存入moves
        moves.push(move);
        towerOfHanoi(plates - 1, helper, source, dest, helperName, sourceName, destName, moves);
      }
      return moves;
    }

    function hanoiStack(plates) {
      // 创建每一个柱子的栈对象，source是最开始拥有所有圈圈的柱子，dest是目标柱子，helper是中间的暂存柱子
      const source = new Stack();
      const dest = new Stack();
      const helper = new Stack();
      //倒序循环把每一个圈圈序号放入source栈
      for (let i = plates; i > 0; i--) {
        source.push(i);
      }
      //通过return调用towerOfHanoi计算方法。
      return towerOfHanoi(plates, source, helper, dest, 'source', 'helper', 'dest');
    }
    //这个方法是计算在汉诺塔的层数为plates的时候，每一个是从哪个柱子拿到哪个柱子的
    function hanoi(plates, source, helper, dest, moves = []) {
      if (plates <= 0) return moves;
      if (plates === 1) {
        moves.push([source, dest]);
      } else {
        hanoi(plates - 1, source, dest, helper, moves);
        moves.push([source, dest]);
        hanoi(plates - 1, helper, source, dest, moves);
      }
      return moves;
    }
    console.log(hanoiStack(3))
    console.log(hanoi(3, 'source', 'helper', 'dest'));
```



# 队列(Queue)

队列(Queue)是一组遵循***先进先出(FIFO)***原则的有序的项,在队尾添加新元素,从队头移除元素.

js创建一个Queue类并使用

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230222094917539.png" alt="image-20230222094917539" style="zoom:80%;" />

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230222094937791.png" alt="image-20230222094937791" style="zoom:80%;" />

代码实现

```
<script>
    class Queue {
      constructor() {
        this.items = {}//利用js的对象存储
        this.count = 0//count属性来记录队列大小
        this.firstCount = 0//用于追踪队列的第一个元素
      }
      //enqueue(element(s)): 向队列尾部添加一个(或多个)新的项。
      enqueue(element) {
        this.items[this.count] = element
        this.count++
      }
      //dequeue(): 移除队列的第一项(即排在队列最前面的项)并返回被移除的元素。
      dequeue() {
        if (this.isEmpty()) {
          return undefined
        }
        const result = this.items[this.firstCount]
        delete this.items[this.firstCount]
        this.firstCount++
        return result
      }
      /* peek(): 返回队列中第一个元素---最先被添加，也将是最先被移除的元素。
      队列不做任何变动(不移除元素，只返回元素信息 - 与stack类的 peek方法非常类似)。该方法在其他语言中也可以叫作front方法。 */
      peek() {
        if (this.isEmpty) {
          return undefined
        }
        return this.items[this.firstCount]
      }
      //isEmpty(): 如果队列中不包含任何元素，返回true，否则返回false。
      isEmpty() {
        return this.count - this.firstCount === 0
      }
      //size(): 返回队列包含的元素个数，与数组的length 属性类似。
      size() {
        return this.count - this.firstCount
      }
      //clear(): 清空队列
      clear() {
        this.items = {}
        this.count = 0
        this.firstCount = 0
      }
      //toString()
      toString() {
        if (this.isEmpty()) {
          return ''
        }
        let objString = `${this.items[this.firstCount]}`
        for (let i = this.firstCount + 1; i < this.count; i++) {
          objString = `${objString},${this.items[i]}`
        }
        return objString
      }
    }
    const queue = new Queue()
    console.log(queue.isEmpty())//true
    queue.enqueue('John')
    queue.enqueue('Jack')
    console.log(queue.toString())//John,Jack
    queue.enqueue('Camila')
    console.log(queue.toString())//John,Jack,Camila
    console.log(queue.size())//3
    console.log(queue.isEmpty())//false
    queue.dequeue()
    queue.dequeue()
    console.log(queue.toString())//Camila
  </script>
```

***双端队列(deque,或称double-ended queue)***,是一种允许我们同时从队头和队尾添加和移除元素的特殊队列

js创建deque并使用

```
<script>
    class Deque {
      constructor() {
        this.items = {}
        this.count = 0
        this.firstCount = 0
      }
      //addFront(element):该方法在双端队列前端添加新的元素
      addFront(element) {
        if (this.isEmpty()) {
          addBack(element)
        } else if (this.firstCount > 0) {
          this.firstCount--
          this.items[this.firstCount] = element
        } else {
          for (let i = this.count; i > 0; i--) {
            this.items[i] = this.items[i - 1]
          }
          this.count++
          this.firstCount = 0
          this.items[0] = element
        }
      }
      //addBack(element):该方法在双端队列后端添加新的元素(实现方法和Queue类中的enqueue方法相同)
      addBack(element) {
        this.items[this.count] = element
        this.count++
      }
      //removeFront():该方法会从双端队列前端移除第一个元素(实现方法和Queue类中的dequeue方法相同)
      removeFront() {
        if (this.isEmpty()) {
          return undefined
        }
        let result = this.items[this.firstCount]
        delete this.items[this.firstCount]
        this.firstCount++
        return result
      }
      //removeBack():该方法会从双端队列后端移除第一个元素(实现方法和Stack类中的pop 方法一样)
      removeBack() {
        if (this.isEmpty()) {
          return undefined
        }
        this.count--
        let result = this.items[this.count]
        delete this.items[this.count]
        return result
      }
      //peekFront():该方法返回双端队列前端的第一个元素(实现方法和 Queue类中的 peek方法一样)
      peekFront() {
        if (this.isEmpty()) {
          return undefined
        }
        return this.items[this.firstCount]
      }
      //peekBack():该方法返回双端队列后端的第一个元素(实现方法和 Stack类中的 peek方法一样)
      peekBack() {
        if (this.isEmpty()) {
          return undefined
        }
        return this.items[this.count - 1]
      }
      isEmpty() {

        return this.count - this.firstCount === 0
      }
      //size(): 返回队列包含的元素个数，与数组的length 属性类似
      size() {
        return this.count - this.firstCount
      }
      //clear(): 清空队列
      clear() {
        this.items = {}
        this.count = 0
        this.firstCount = 0
      }
      //toString()
      toString() {
        if (this.isEmpty()) {
          return ''
        }
        let objString = `${this.items[this.firstCount]}`
        for (let i = this.firstCount + 1; i < this.count; i++) {
          objString = `${objString},${this.items[i]}`
        }
        return objString
      }
    }
    const deque = new Deque();
    console.log(deque.isEmpty()); // 输出 true
    deque.addBack('John');
    deque.addBack('Jack');
    console.log(deque.toString()); //John, Jack
    deque.addBack('Camila');
    console.log(deque.toString()); // John, Jack, Camila
    console.log(deque.size());// 输出3
    console.log(deque.isEmpty());// 输出 false
    deque.removeFront();//移除John
    console.log(deque.toString()); // Jack, Camila
    deque.removeBack();// Camila 决定离开
    console.log(deque.toString());// Jack
    deque.addFront('John');//John 回来询问一些信息
    console.log(deque.toString()); // John, Jack
  </script>
```

***案例(击鼓传花游戏)***

其中队列构造使用之前构造的Queue类(这里省略,实际运行时要加上)

注意:当此轮淘汰一人后,下一轮由此次淘汰人员的下一位开始传递

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230222142214561.png" alt="image-20230222142214561" style="zoom: 67%;" />

```
function hotPotato(elementsList, num) {//elementsList:参与游戏的人员;num:传递次数
      const queue = new Queue()
      const elimitatedList = []//保存淘汰人员
      for (let i = 0; i < elementsList.length; i++) {
        queue.enqueue(elementsList[i])
      }
      while (queue.size() > 1) {
        for (let i = 0; i < num; i++) {
          queue.enqueue(queue.dequeue())
        }
        elimitatedList.push(queue.dequeue())
      }
      return {
        elimitated: elimitatedList,
        winner: queue.dequeue()
      }
    }
    const names = ['John', 'Jack', 'Camila', 'Ingrid', 'Carl']
    const result = hotPotato(names, 7)
    result.elimitated.forEach(name => {
      console.log(`${name}在击鼓传花游戏中被淘汰`)
    })
    console.log("胜利者:", result.winner)
```

***案例(回文检查器)***

注意:回文是指正反都能读通的单词,词组,数或一系列字符的序列;如 madam 或 racecar

```
function palindromeChecker(aString) {
      if (aString === undefined || aString === null || aString != null && aString === 0) {
        return false
      }
      const deque = new Deque()
      const lowerString = aString.toLocaleLowerCase().split(" ").join('')
      let isEqual = true
      let firstChar, lastChar
      for (let i = 0; i < lowerString.length; i++) {
        deque.addBack(lowerString.charAt(i))
      }
      while (deque.size() > 1 && isEqual) {
        firstChar = deque.removeFront()
        lastChar = deque.removeBack()
        if (firstChar != lastChar) {
          isEqual = false
        }
      }
      return isEqual
    }
    console.log('a', palindromeChecker('a'))
    console.log('aa', palindromeChecker('aa'))
    console.log('kayak', palindromeChecker('kayak'))
    console.log('Was it a car or a cat I saw', palindromeChecker('Was it a car or a cat I saw'))
```

# 集合(Set)

集合是由一组无序的且唯一的(即不能重复的)项组成的

**代码实现**:

(ES6新增了Set,我们可直接使用Set及其方法;下列代码只是模拟Set类的构造及其部分方法)

```
<script>
    class Set {
      constructor() {
        this.items = {}
      }
      //add(element):向集合中添加一个元素
      add(element) {
        if (!this.has(element)) {
          this.items[element] = element
          return true
        }
        return false
      }
      //delete(element):从集合中移除一个元素
      delete(element) {
        if (this.has(element)) {
          delete this.items[element]
          return true
        }
        return false
      }
      //has(element):如果元素在集合中返回true;如果不在返回false
      has(element) {
        return Object.prototype.hasOwnProperty.call(this.items, element)
      }
      //clear():移除集合中的所有元素
      clear() {
        return items = {}
      }
      //size():返回集合中所包含的元素个数,和length类似
      size() {
        return Object.keys(this.items).length
      }
      //values():返回一个包含集合中所有值的数组
      values() {
        return Object.values(this.items)
      }
    }
    const set = new Set()
    set.add(1)
    console.log(set.values())//true
    console.log(set.has(1))//[1]
    console.log(set.size())//1
    set.add(2)
    console.log(set.values())//[1,2]
    console.log(set.has(2))//true
    console.log(set.size())//2
    set.delete(1)
    console.log(set.values())//[2]
    set.delete(2)
    console.log(set.values())//[]
  </script>
```

下面是ES6中的Set类,和我们模拟的set类有所不同

```
const set = new Set()
    set.add(1)
    set.add(2)
    console.log(set.values())//SetIterator {1, 2}
    console.log(set.has(1))//true
    console.log(set.size)//2
    set.delete(1)
    console.log(set.values())//SetIterator {2}
```



## 集合运算

并集:对于给定的两个集合,返回一个包含两个集合中所有元素的新集合

交集:对于给定的两个集合,返回一个包含两个集合中共有元素的新集合

差集:对于给定的两个集合,返回一个包含所有元素存在于第一个集合但不存在于第二个集合的新集合

子集:验证一个给定集合是否是另一个集合的子集

**代码实现**:(在之前模拟构造的Set类中新增加了4个方法

union(otherSet),

interSection(otherSet),

difference(otherSet),

isSubsetOf(otherSet))

```
<script>
    class Set {
      constructor() {
        this.items = {}
      }
      //add(element):向集合中添加一个元素
      add(element) {
        if (!this.has(element)) {
          this.items[element] = element
          return true
        }
        return false
      }
      //delete(element):从集合中移除一个元素
      delete(element) {
        if (this.has(element)) {
          delete this.items[element]
          return true
        }
        return false
      }
      //has(element):如果元素在集合中返回true;如果不在返回false
      has(element) {
        return Object.prototype.hasOwnProperty.call(this.items, element)
      }
      //clear():移除集合中的所有元素
      clear() {
        return items = {}
      }
      //size():返回集合中所包含的元素个数,和length类似
      size() {
        return Object.keys(this.items).length
      }
      //values():返回一个包含集合中所有值的数组
      values() {
        return Object.values(this.items)
      }
      //union(otherSet):并集
      union(otherSet) {
        const unionSet = new Set()
        this.values().forEach(value => unionSet.add(value))
        otherSet.values().forEach(value => unionSet.add(value))
        return unionSet
      }
      //interSection(otherSet):交集
      interSection(otherSet) {
        const interSectionSet = new Set()
        const values = this.values()
        for (let i = 0; i < values.length; i++) {
          if (otherSet.has(values[i])) {
            interSectionSet.add(values[i])
          }
        }
        return interSectionSet
      }
      //difference(otherSet):差集(例如setA.difference(setB)的结果是存在于setA中却不存在于setB中的元素)
      difference(otherSet) {
        const differenceSet = new Set()
        const values = this.values()
        values.forEach(value => {
          if (!otherSet.has(value)) {
            differenceSet.add(value)
          }
        })
        return differenceSet
      }
      //isSubsetOf(otherSet):子集(setA.isSubsetOf(setB)验证setA是否是setB的子集)
      isSubsetOf(otherSet) {
        if (this.size() > otherSet.size()) {
          return false
        }
        let isSubset = true
        this.values().every(value => {
          if (!otherSet.has(value)) {
            isSubset = false
            return false
          }
          return true
        })
        return isSubset
      }
    }
    const setA = new Set()
    setA.add(1)
    setA.add(2)
    setA.add(3)
    const setB = new Set()
    setB.add(3)
    setB.add(4)
    setB.add(5)
    setB.add(6)
    const setC = new Set()
    setC.add(3)
    setC.add(5)
    const unionSetAB = setA.union(setB)
    const interSectionSetAB = setA.interSection(setB)
    const differenceSetAB = setA.difference(setB)
    console.log(unionSetAB.values())
    console.log(interSectionSetAB.values())
    console.log(differenceSetAB.values())
    console.log(setC.isSubsetOf(setB))
  </script>
```

使用扩展运算符模拟集合运算

```
const setA = new Set()
    setA.add(1)
    setA.add(2)
    setA.add(3)
    const setB = new Set()
    setB.add(3)
    setB.add(4)
    setB.add(5)
    setB.add(6)
    //模拟并集
    console.log(new Set([...setA, ...setB]))//Set(6) {1, 2, 3, 4, 5, 6}
    //模拟交集
    console.log(new Set([...setA].filter(x => setB.has(x))))//Set(1) {3}
    //模拟差集
    console.log(new Set([...setA].filter(x => !setB.has(x))))//Set(2) {1, 2}
```

# 字典和散列表(Map类)

集合是一组互不相同的元素,它是以[值,值]形式来存储元素;字典是以[键,值]对形式来存储元素

## 字典(Map类)

代码实现(以ES6中的Map类为基础)

```
<script>
    function defaultToString(item) {
      if (item == null) {
        return 'NULL'
      } else if (item == undefined) {
        return 'UNDEFINED'
      } else if (typeof item == 'string' || item instanceof String) {
        return `${item}`
      } else {
        return item.toString()
      }
    }
    class ValuePair {
      constructor(key, value) {
        this.key = key
        this.value = value
      }
      toString() {
        return `[${this.key}:${this.value}]`
      }
    }
    class Dictionary {
      constructor(toStrFn = defaultToString) {
        this.toStrFn = toStrFn
        this.table = {}
      }
      //set(key,value):像字典中添加新的键值对,如果键名已存在,那么其对应的值会被新值覆盖
      set(key, value) {
        if (key !== null && value !== null) {
          const tableKey = this.toStrFn(key)
          this.table[tableKey] = new ValuePair(key, value)
          return true
        }
        return false
      }
      //remove(key):通过键值作为参数移除字典中对应的数据值
      remove(key) {
        if (this.hasKey(key)) {
          delete this.table[this.toStrFn(key)]
          return true
        }
        return false
      }
      //hasKey(key):如果某个键值存在于字典中,返回true,否则返回false
      hasKey(key) {
        return this.table[this.toStrFn(key)] !== null
      }
      //get(key):通过以键值作为参数查找特定数值并返回
      get(key) {
        const valuePair = this.table[this.toStrFn(key)]
        return valuePair == null ? undefined : valuePair.value
      }
      //clear():删除该字典中的所有值
      clear() {
        this.table = {}
      }
      //size():返回字典中所包含的值的数量,和数组的length相似
      size() {
        return Object.keys(this.table).length
      }
      //isEmpty():size等于0时返回true,否则返回false
      isEmpty() {
        return this.size === 0
      }
      //keys():将字典所包含的键名以数组形式返回
      keys() {
        return this.keyValues().map(valuePair => valuePair.key)
      }
      //values():将字典所包含的值以数组形式返回
      values() {
        return this.keyValues().map(valuePair => valuePair.value)
      }
      //keyValues():将字典中的所有[键,值]对返回
      keyValues() {
        return Object.values(this.table)
      }
      //forEach(callbackFn):迭代字典中所有键值对,callbackFn两个参数key和value;该方法在回调函数返回值false终止
      forEach(callbackFn) {
        const valuePair = this.keyValues()
        for (let i = 0; i < valuePair.length; i++) {
          const result = callbackFn(valuePair[i].key, valuePair[i].value)
          if (result === false) {
            break
          }
        }
      }
      //toString()
      toString() {
        if (this.isEmpty()) {
          return ''
        }
        const valuePair = this.keyValues()
        let objString = `${valuePair[0].toString()}`
        for (let i = 1; i < valuePair.length; i++) {
          objString = `${objString},${valuePair[i].toString()}`
        }
        return objString
      }
    }
    const dictionary = new Dictionary()
    dictionary.set('Gandalf', 'gandalf@email.com')
    dictionary.set('John', 'johnSnow@email.com')
    dictionary.set('Tyrion', 'tyrion@email.com')
    console.log(dictionary.hasKey('Gandalf'))//true
    console.log(dictionary.size())//3
    console.log(dictionary.keys())//['Gandalf', 'John', 'Tyrion']
    console.log(dictionary.values())//['gandalf@email.com', 'johnSnow@email.com', 'tyrion@email.com']
    console.log(dictionary.get('Tyrion'))//tyrion@email.com
    dictionary.remove('John')
    console.log(dictionary.keys())// ['Gandalf', 'Tyrion']
    console.log(dictionary.values())//['gandalf@email.com', 'tyrion@email.com']
    console.log(dictionary.keyValues())
    //{key: 'Gandalf', value: 'gandalf@email.com'}
    //{key: 'Tyrion', value: 'tyrion@email.com'}
    dictionary.forEach((k, v) => {
      console.log('forEach:', `key:${k},value:${v}`)
    })
    //forEach: key:Gandalf,value:gandalf@email.com
    //forEach: key:Tyrion,value:tyrion@email.com
  </script>
```

## 散列表(hashMap)

散列算法的作用是尽可能地在数据结构中找到一个值;在之前的数据结构中如果想要获得一个值,就需要迭代整个数据结构,如果使用散列函数,就知道值的具体位置,因此能够快速检索到该值

散列函数的作用是给定一个键值,然后返回只在表中的地址

代码实现

```
  <script>
    function defaultToString(item) {
      if (item == null) {
        return 'NULL'
      } else if (item == undefined) {
        return 'UNDEFINED'
      } else if (typeof item == 'string' || item instanceof String) {
        return `${item}`
      } else {
        return item.toString()
      }
    }
    class ValuePair {
      constructor(key, value) {
        this.key = key
        this.value = value
      }
      toString() {
        return `[${this.key}:${this.value}]`
      }
    }
    class HashTable {
      constructor(toStrFn = defaultToString) {
        this.toStrFn = toStrFn
        this.table = {}
      }
      //创建散列函数
      loseloseHashCode(key) {
        if (typeof key === 'number') {
          return key
        }
        const tableKey = this.toStrFn(key)
        let hash = 0
        for (let i = 0; i < tableKey.length; i++) {
          hash += tableKey.charCodeAt(i)
        }
        return hash % 37
      }
      hashCode(key) {
        return this.loseloseHashCode(key)
      }
      //put(key,value):向散列表增加一个新的项
      put(key, value) {
        if (key !== null && value !== null) {
          const position = this.hashCode(key)
          this.table[position] = new ValuePair(key, value)
          return true
        }
        return false
      }
      //remove(key):根据键值从散列表中移除
      remove(key) {
        const hash = this.hashCode(key)
        const valuePair = this.table[hash]
        if (valuePair !== null) {
          delete this.table[hash]
          return true
        }
        return false
      }
      //get(key):返回根据键值检索到的特定的值
      get(key) {
        const valuePair = this.table[this.hashCode(key)]
        return valuePair == null ? undefined : valuePair.value
      }
    }
    const hash = new HashTable()
    hash.put('Gandalf', 'gandalf@email.com')
    hash.put('John', 'johnSnow@email.com')
    hash.put('Tyrion', 'tyrion@email.com')
    console.log(hash.hashCode('Gandalf') + '-Gandalf')//19-Gandalf
    console.log(hash.hashCode('John') + '-John')//29-John
    console.log(hash.hashCode('Tyrion') + '-Tyrion')//16-Tyrion
    console.log(hash.get('Gandalf'))//gandalf@email.com
    console.log(hash.get('Loiane'))//undefined
    hash.remove('GanDalf')
    console.log(hash.get('Gandalf'))//gandalf@email.com
  </script>
```

## 处理散列表中的冲突

有些时候某些键会有相同的散列值,不同的值在散列表中对应相同的位置的时候我们称其为冲突

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230228142438027.png" alt="image-20230228142438027" style="zoom:80%;" />

代码如下:

```
<script>
    function defaultToString(item) {
      if (item == null) {
        return 'NULL'
      } else if (item == undefined) {
        return 'UNDEFINED'
      } else if (typeof item == 'string' || item instanceof String) {
        return `${item}`
      } else {
        return item.toString()
      }
    }
    class ValuePair {
      constructor(key, value) {
        this.key = key
        this.value = value
      }
      toString() {
        return `[${this.key}:${this.value}]`
      }
    }
    class HashTable {
      constructor(toStrFn = defaultToString) {
        this.toStrFn = toStrFn
        this.table = {}
      }
      //创建散列函数
      loseloseHashCode(key) {
        if (typeof key === 'number') {
          return key
        }
        const tableKey = this.toStrFn(key)
        let hash = 0
        for (let i = 0; i < tableKey.length; i++) {
          hash += tableKey.charCodeAt(i)
        }
        return hash % 37
      }
      hashCode(key) {
        return this.loseloseHashCode(key)
      }
      //put(key,value):向散列表增加一个新的项
      put(key, value) {
        if (key !== null && value !== null) {
          const position = this.hashCode(key)
          this.table[position] = new ValuePair(key, value)
          return true
        }
        return false
      }
      //remove(key):根据键值从散列表中移除
      remove(key) {
        const hash = this.hashCode(key)
        const valuePair = this.table[hash]
        if (valuePair !== null) {
          delete this.table[hash]
          return true
        }
        return false
      }
      //get(key):返回根据键值检索到的特定的值
      get(key) {
        const valuePair = this.table[this.hashCode(key)]
        return valuePair == null ? undefined : valuePair.value
      }
      //
      isEmpty() {
        return this.size === 0
      }
      //toString()
      toString() {
        if (this.isEmpty()) {
          return ''
        }
        const keys = Object.keys(this.table)
        let objString = `${keys[0]}=>${this.table[keys[0]].toString()}`
        for (let i = 1; i < keys.length; i++) {
          objString = `${objString},${keys[i]}=>${this.table[keys[i]].toString()}`
        }
        return objString
      }
    }
    const hash = new HashTable()
    hash.put('Ygritte', 'Ygritte@email.com')
    hash.put('Jonathan', 'Jonathan@email.com')
    hash.put('Jamie', 'Jamie@email.com')
    hash.put('Jack', 'Jack@email.com')
    hash.put('Jasmine', 'Jasmine@email.com')
    hash.put('Jake', 'Jake@email.com')
    hash.put('Nathan', 'Nathan@email.com')
    hash.put('Athelstan', 'athelstan@email.com')
    hash.put('Sue', 'Sue@email.com')
    hash.put('Aethelwulf', 'aethelwulf@email.com')
    hash.put('Sargeras', 'Sargeras@email.com')
    console.log(hash.hashCode('Ygritte') + '-Ygritte')//4-Ygritte
    console.log(hash.hashCode('Jonathan') + '-Jonathan')//5-Jonathan
    console.log(hash.hashCode('Jamie') + '-Jamie')//5-Jamie
    console.log(hash.hashCode('Jack') + '-Jack')//7-Jack
    console.log(hash.hashCode('Jasmine') + '-Jasmine')//8-Jasmine
    console.log(hash.hashCode('Jake') + '-Jake')//9-Jake
    console.log(hash.hashCode('Nathan') + '-Nathan')//10-Nathan
    console.log(hash.hashCode('Athelstan') + '-Athelstan')//7-Athelstan
    console.log(hash.hashCode('Sue') + '-Sue')//5-Sue
    console.log(hash.hashCode('Aethelwulf') + '-Aethelwulf')//5-Aethelwulf
    console.log(hash.hashCode('Sargeras') + '-Sargeras')//10-Sargeras
    console.log(hash.toString())
  </script>
```

#### 解决方法1:**分离链接法**

分离链接法包括为散列表的每一个位置创建一个链表并将元素存储在里面,它是解决冲突最简单的办法,但需要额外的空间

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230228162031935.png" alt="image-20230228162031935" style="zoom:80%;" />

代码实现(代码中需要用到之前的LinkedList数据结构,这里仅展示需要重写的put,remove,get方法)

```
put(key, value) {
        if (key !== null && value !== null) {
          const position = this.hashCode(key)
          if (this.table[position] == null) {
            this.table[position] = new LinkedList()
          }
          this.table[position].push(new ValuePair(key, value))
          return true
        }
        return false
      }
      get(key) {
        const position = this.hashCode(key)
        const linkedList = this.table[position]
        if (linkedList != null && !linkedList.isEmpty()) {
          let current = linkedList.getHead()
          while (current != null) {
            if (current.element.key === key) {
              return current.element.value
            }
            current = current.next
          }
        }
        return undefined
      }
      remove(key) {
        const position = this.hashCode(key)
        const linkedList = this.table[position]
        if (linkedList != null && !linkedList.isEmpty()) {
          let current = linkedList.getHead()
          while (current != null) {
            if (current.element.key === key) {
              linkedList.remove(current.element)
              if (linkedList.isEmpty()) {
                delete this.table[position]
              }
              return true
            }
            current = current.next
          }
        }
        return false
      }
```

测试代码及结果如图

```
const hash = new HashTableSeparateChaining()
    hash.put('Ygritte', 'Ygritte@email.com')
    hash.put('Jonathan', 'Jonathan@email.com')
    hash.put('Jamie', 'Jamie@email.com')
    hash.put('Jack', 'Jack@email.com')
    hash.put('Jasmine', 'Jasmine@email.com')
    hash.put('Jake', 'Jake@email.com')
    hash.put('Nathan', 'Nathan@email.com')
    hash.put('Athelstan', 'athelstan@email.com')
    hash.put('Sue', 'Sue@email.com')
    hash.put('Aethelwulf', 'aethelwulf@email.com')
    hash.put('Sargeras', 'Sargeras@email.com')
    console.log(hash.toString())
    hash.remove('Aethelwulf')
    hash.remove('Sargeras')
    console.log(hash.toString())
    console.log(hash.get('Sue'))
```

![image-20230228161537613](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230228161537613.png)

#### 解决方法2:**线性探查法**

之所以叫线性,是因为它的处理方法是直接将数据存到表中,而不是在单独的数据结构中

当你想往表中的某个位置添加一个新元素时,如果索引为position的位置已经被占用,就尝试position+1位置,如果该位置也被占据就尝试position+2位置,以此类推,直到找到一个空闲位置

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230228162419668.png" alt="image-20230228162419668" style="zoom:80%;" />

线性探查技术分两种

第一种软删除方法,我们使用一个特殊值标记键值对被删除了,而不是真的删除它;经过一段时间后我们会得到一个有若干标记删除位置的散列表;这样会导致随时间的增加,散列表的效率逐渐降低

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230228163323164.png" alt="image-20230228163323164" style="zoom:80%;" />

第二种方法需检验有无必要将一个或多个元素移动到之前的位置

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230228163526479.png" alt="image-20230228163526479" style="zoom:80%;" />



# 树(Tree)

## 认识递归

递归通常涉及调用函数自身,每个递归函数都要有一个基线条件,即一个不再递归条件(停止点),避免无限递归

### 案例:一个数的阶乘

​	迭代阶乘

```
function factorialIterative(number) {
      if (number < 0) {
        return undefined
      } else {
        for (let i = number - 1; i > 0; i--) {
          number = number * i
        }
      }
      return number
    }
    console.log(factorialIterative(5))//120
```

​	递归阶乘

```
function factorial(number) {
      if (number === 1) {
        return 1
      } else if (number === 0) {
        return undefined
      } else {
        return number * factorial(number - 1)
      }
    }
    console.log(factorial(5))//120
    console.log(factorial(0))//undefined
    console.log(factorial(1))//1
```

### 案例二:斐波那契数列

​	迭代

```
function fibonacciIterative(n) {
      if (n === 0) {
        return 0
      } else if (n <= 2) {
        return 1
      } else {
        let n1 = 1
        let n2 = 2
        let fin = 0
        for (let i = 3; i < n; i++) {
          fin = n1 + n2
          n1 = n2
          n2 = fin
        }
        return fin
      }

    }
    console.log(fibonacciIterative(6))//8
```

​	递归

```
function fibonacci(n) {
      if (n === 0) return 0
      if (n <= 2) return 1
      return fibonacci(n - 1) + fibonacci(n - 2)
    }
    console.log(fibonacci(6))//8
```

## 树相关术语

树是非顺序数据结构

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230302143850851.png" alt="image-20230302143850851" style="zoom:80%;" />

位于树顶的叫**根节点**,它没有父节点,树中的每个元素都叫节点,分为**内部节点**和**外部节点**,没有子元素的节点称作外部节点(叶子节点),至少有一个子节点的为内部节点;**子树**是由节点和它的后代构成;节点的**深度**取决于它祖先结点的个数;**树的高度**取决于所有节点深度的最大值

**二叉树**中的节点最多只能有两个子节点;一个是左侧节点一个是右侧节点;

**二叉搜索树(BST)**是二叉树的一种;但它只允许在左侧节点存储(比父节点)小的值,在右侧节点存储(比父节点)大的值

## 创建BST

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230302164316226.png" alt="image-20230302164316226" style="zoom:80%;" />

```
const Compare = {
      LESS_THAN: -1,
      BIGGER_THAN: 1,
      EQUALS: 0
    };
    //声明一个方法来比较节点值，判断元素存储到左侧节点还是右侧节点
    function defaultCompare(a, b) {
      if (a === b) {
        return Compare.EQUALS;
      }
      return a < b ? Compare.LESS_THAN : Compare.BIGGER_THAN;
    }
    //表示每个节点
    class Node {
      constructor(key) {
        this.key = key
        this.left = null
        this.right = null
      }
    }
    class BinarySearchTree {
      constructor(compareFn = defaultCompare) {
        this.compareFn = compareFn
        this.root = null
      }
      //insert(key):向树中插入一个新的键
      insertNode(node, key) {
        if (this.compareFn(key, node.key) === Compare.LESS_THAN) {
          if (node.left == null) {
            node.left = new Node(key)
          } else {
            this.insertNode(node.left, key)
          }
        } else {
          if (node.right == null) {
            node.right = new Node(key)
          } else {
            this.insertNode(node.right, key)
          }
        }
      }
      insert(key) {
        if (this.root == null) {
          this.root = new Node(key)
        } else {
          this.insertNode(this.root, key)
        }
      }
     }
    const tree = new BinarySearchTree()
    tree.insert(11)
    tree.insert(7)
    tree.insert(15)
    tree.insert(5)
    tree.insert(3)
    tree.insert(9)
    tree.insert(8)
    tree.insert(10)
    tree.insert(13)
    tree.insert(12)
    tree.insert(14)
    tree.insert(20)
    tree.insert(18)
    tree.insert(25)
    tree.insert(6)
```



## 树的遍历(以BST为例)

中序遍历:一种以上行顺序访问BST所有结点的遍历方式;它是从最小节点到最大结点的遍历顺序

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230302164518018.png" alt="image-20230302164518018" style="zoom:80%;" />

```
//inOrderTraverse():中序遍历所有节点
      inOrderTraverse(callback) {
        this.inOrderTraverseNode(this.root, callback)
      }
      inOrderTraverseNode(node, callback) {
        if (node != null) {
          this.inOrderTraverseNode(node.left, callback)
          callback(node.key)
          this.inOrderTraverseNode(node.right, callback)
        }
      }
```

先序遍历:以优先于后代节点的顺序访问每个节点

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230302165221038.png" alt="image-20230302165221038" style="zoom:80%;" />

```
//preOrderTraverse():先序遍历所有节点
      preOrderTraverse(callback) {
        this.preOrderTraverseNode(this.root, callback)
      }
      preOrderTraverseNode(node, callback) {
        if (node != null) {
          callback(node.key)
          this.preOrderTraverseNode(node.left, callback)
          this.preOrderTraverseNode(node.right, callback)
        }
      }
```

后序遍历:先访问节点的后代节点,再访问节点本身

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230302165444000.png" alt="image-20230302165444000" style="zoom:80%;" />

```
//postOrderTraverse():后序遍历所有节点
      postOrderTraverse(callback) {
        this.postOrderTraverseNode(this.root, callback)
      }
      postOrderTraverseNode(node, callback) {
        if (node != null) {
          this.postOrderTraverseNode(node.left, callback)
          this.postOrderTraverseNode(node.right, callback)
          callback(node.key)
        }
      }
```

## 搜索树中的值(以BST为例)

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230303131043942.png" alt="image-20230303131043942" style="zoom:80%;" />

从上图容易看到该树最后一层最左侧的节点3是最小值;最右侧节点25是最大值;

因此对于寻找最小值,总是沿着树的最左边;对于寻找最大值,总是沿着树的最右边

最小值搜索:

```
//min():返回树中最小值
      minNode(node) {
        let current = node
        while (current != null && current.left != null) {
          current = current.left
        }
        return current
      }
      min() {
        return this.minNode(this.root)
      }
```

最大值搜索:

```
//max():返回树中最大值
      maxNode(node) {
        let current = node
        while (current != null && current.right != null) {
          current = current.right
        }
        return current
      }
      max() {
        return this.maxNode(this.root)
      }
```

搜索特定值:

```
//search(key):在树中查找一个键;如果节点存在返回true;不存在返回false
      searchNode(node, key) {
        if (node == null) {
          return false
        } else if (this.compareFn(key, node.key) == Compare.LESS_THAN) {
          return this.searchNode(node.left, key)
        } else if (this.compareFn(key, node.key) == Compare.BIGGER_THAN) {
          return this.searchNode(node.right, key)
        } else {
          return true
        }
      }
      search(key) {
        return this.searchNode(this.root, key)
      }
```

## 移除一个节点(以BST为例)

分三种情况

移除一个没有后代节点的节点,只需将该节点为null并返回该节点

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230303134705830.png" alt="image-20230303134705830" style="zoom:80%;" />



移除有一个左侧节点或右侧节点的节点,需要将对该节点的引用改为对其左侧节点(或右侧节点)的引用,并返回更新后的节点

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230303134726603.png" alt="image-20230303134726603" style="zoom:80%;" />

移除有两个子节点的节点

首先找到该节点右侧子树中的最小节点(继承者)

然后用这个最小节点替换当前需要移除的节点(此时该节点被移除),同时将右侧子树中的最小节点移除

最后返回更新后的节点的引用

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230303135324728.png" alt="image-20230303135324728" style="zoom:80%;" />

```
//remove(key):移除某个键
      remove(key) {
        this.root = this.removeNode(this.root, key)
        return this.root
      }
      removeNode(node, key) {
        if (node == null) {
          return null
        }
        if (this.compareFn(key, node.key) === Compare.LESS_THAN) {
          node.left = this.removeNode(node.left, key)
          return node
        } else if (this.compareFn(key, node.key) === Compare.BIGGER_THAN) {
          node.right = this.removeNode(node.right, key)
          return node
        } else {
          //第一种情况
          if (node.left == null && node.right == null) {
            node = null
            return node
          }
          //第二种情况
          if (node.left == null) {
            node = node.right
            return node
          } else if (node.right == null) {
            node = node.left
            return node
          }
          //第三种情况
          const aux = this.minNode(node.right)
          node.key = aux.key
          node.right = this.removeNode(node.right, aux.key)
          return node
        }
      }
```

