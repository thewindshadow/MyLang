## 排序算法（Java）——那些年面试常见的排序算法

来源：[https://segmentfault.com/a/1190000013826611](https://segmentfault.com/a/1190000013826611)


## 前言

　　排序就是将一组对象按照某种逻辑顺序重新排列的过程。比如信用卡账单中的交易是按照日期排序的——这种排序很可能使用了某种排序算法。在计算时代早期，大家普遍认为30%的计算周期都用在了排序上，今天这个比例可能降低了，大概是因为现在的排序算法更加高效。现在这个时代数据可以说是无处不在，而整理数据的第一步往往就是进行排序。所有的计算机系统都实现了各种排序算法以供系统和用户使用。
　　即使你只是使用标准库中的排序函数，学习排序算法仍然有很大的实际意义：


* 排序算法往往是我们解决其他问题的第一步
* 排序算法有助于我们理解其他算法
* 算法在公司面试中占有很大比例，排序算法作为其中的重要组成部分，我们理所当然要学好了。


　　另外，更重的是下面介绍的这些算法都很经典，优雅而且高效，学习其中的精髓对自己提高自己的编程能力也有很大的帮助。
　　排序在商业数据处理和现代科学计算中有很重要的地位，它能够应用于事务处理,组合优化，天体物理学，分子动力学，语言学，基因组学，天气预报和很多其他领域。下面会介绍的一种排序算法（快速排序）甚至被誉为20世纪科学和工程领域的十大算法之一。后面我们会依次学习几种经典的排序算法，并高效地实现“优先队列”这种基础数据类型。我们将讨论比较排序算法的理论基础并中借若干排序算法和优先队列的应用。
## 第一章——初始初级排序算法
## 一，我知道的第一个排序算法——冒泡排序
### 1. 介绍:　

　  这是比较简单的一种的排序算法，应该是我们大学最先接触到的一个排序算法了。很简单的一种排序算法，大学里好像也是每次必考的吧！
### 2. 原理:

　　比较相邻的元素。如果第一个比第二个大，就交换他们两个。 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。针对所有的元素重复以上的步骤，除了最后一个。持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。 
代码实现：
### 3. 实现代码

```java
    public static void bubbleSort(int[] numbers) {
        int temp = 0;
        int size = numbers.length;
        for (int i = 0; i < size - 1; i++) {
            for (int j = 0; j < size - 1 - i; j++) {
                 // 交换两数位置
                if (numbers[j] > numbers[j + 1])
                {
                    temp = numbers[j];
                    numbers[j] = numbers[j + 1];
                    numbers[j + 1] = temp;
                }
            }
        }
    }
```
## 二，另一个简单排序算法——选择排序
### 1. 介绍:　

　  选择排序市一中很容易理解和实现的简单排序算法。学习它之前首先要知道它的两个很鲜明的特点。


* **`运行时间和输入无关`** 。为了找出最小的元素而扫描一遍数组并不能为下一遍扫描提供任何实质性帮助的信息。因此使用这种排序的我们会惊讶的发现，一个已经有序的数组或者数组内元素全部相等的数组和一个元素随机排列的数组所用的排序时间竟然一样长！而其他算法会更善于利用输入的初始状态，选择排序则不然。
* **`数据移动是最少的`** 选择排序的交换次数和数组大小关系是线性关系。看下面的原理时可以很容易明白这一点。


### 2. 原理:

　　在要排序的一组数中，选出最小的一个数与第一个位置的数交换；然后在剩下的数当中再找最小的与第二个位置的数交换，如此循环到倒数第二个数和最后一个数比较为止。类似下图：


![][0] 
代码实现：
### 3. 实现代码

```java
    public static void selectSort(int[] numbers) {
        // 数组长度
        int size = numbers.length; 
        // 中间变量
        int temp = 0; 

        for (int i = 0; i < size; i++) {
            // 待确定的位置
            int k = i; 
            // 选择出应该在第i个位置的数
            for (int j = size - 1; j > i; j--) {
                if (numbers[j] < numbers[k]) {
                    k = j;
                }
            }
            // 交换两个数
            temp = numbers[i];
            numbers[i] = numbers[k];
            numbers[k] = temp;
        }
    }
```
## 三，另一个简单排序算法——插入排序
### 1. 介绍:　

　　通常人们整理桥牌的方法是一张一张的来，将每一张牌插入到其他已经有序牌中的适当位置。在计算机的实现中，为了给要插入的元素腾出空间，我们需要将其余所有元素在插入之前都向右移动以为。这种算法就叫插入排序。
　**　与选择排序一样，当前索引左边的所有元素都是有序的，但他们的最终位置还不确定为了给更小的元素腾出空间，他们可能会被移动。但是当索引到达数组的右端时，数组排序就完成了。
　　和选择排序不同的是，插入排序所需的时间取决于输入中元素的初始顺序。也就是说对一个接近有序或有序的数组进行排序会比随机顺序或是逆序的数组进行排序要快的多。**
### 2. 原理:　

　　每步将一个待排序的记录，按其顺序码大小插入到前面已经排序的字序列的合适位置（从后向前找到合适位置后），直到全部插入排序完为止。类似下图：
　　


![][1]
### 3. 实现代码

```java
    /**
     * 插入排序
     * 
     * 从第一个元素开始，该元素可以认为已经被排序 取出下一个元素，在已经排序的元素序列中从后向前扫描
     * 如果该元素（已排序）大于新元素，将该元素移到下一位置 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置 将新元素插入到该位置中 重复步骤2
     * 
     * @param numbers
     *            待排序数组
     */
    public static void insertSort(int[] numbers) {
        int size = numbers.length;
        int temp = 0;
        int j = 0;

        for (int i = 0; i < size; i++) {
            temp = numbers[i];
            // 假如temp比前面的值小，则将前面的值后移
            for (j = i; j > 0 && temp < numbers[j - 1]; j--) {
                numbers[j] = numbers[j - 1];
            }
            numbers[j] = temp;
        }
    }
```
## 四，希尔排序
### 1. 介绍:

　　这个排序咋一看名字感觉很高大上，这是以 **`D.L.shell`** 名字命名的排序算法。
　　为了展示初级排序算法性质的价值，我们来看一下 **`基于插入排序的快速的排序算法——希尔排序`** 。对于大规模乱序的数组插入排序很慢，因为它只会交换相邻的元素，因此元素只能一点一点地从数组的一端移动到另一端。如果最小的元素刚好在数组的尽头的话，那么要将它移动到正确的位置要N-1次移动。希尔排序为了加快速度简单地改进了插入排序，交换不相邻的元素以对数组的局部进行排序，并最终用插入排序将局部有序的数组排序。
### 2. 原理:

先将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序，待整个序列中的记录“基本有序”时，再对全体记录进行依次直接插入排序。
### 3. 实现代码

```java
 /**
     * 希尔排序的原理:根据需求，如果你想要结果从大到小排列，它会首先将数组进行分组，然后将较大值移到前面，较小值
     * 移到后面，最后将整个数组进行插入排序，这样比起一开始就用插入排序减少了数据交换和移动的次数，可以说希尔排序是加强 版的插入排序 拿数组5, 2,
     * 8, 9, 1, 3，4来说，数组长度为7，当increment为3时，数组分为两个序列
     * 5，2，8和9，1，3，4，第一次排序，9和5比较，1和2比较，3和8比较，4和比其下标值小increment的数组值相比较
     * 此例子是按照从大到小排列，所以大的会排在前面，第一次排序后数组为9, 2, 8, 5, 1, 3，4
     * 第一次后increment的值变为3/2=1,此时对数组进行插入排序， 实现数组从大到小排
     */

    public static void shellSort(int[] data) {
        int j = 0;
        int temp = 0;
        // 每次将步长缩短为原来的一半
        for (int increment = data.length / 2; increment > 0; increment /= 2) {
            for (int i = increment; i < data.length; i++) {
                temp = data[i];
                for (j = i; j >= increment; j -= increment) {
                   // 如想从小到大排只需修改这里
                    if (temp > data[j - increment])
                    {
                        data[j] = data[j - increment];
                    } else {
                        break;
                    }

                }
                data[j] = temp;
            }

        }
    }
```
## 第二章——进阶之归并排序
### 1, 介绍

　　归并即将两个有序的数组归并并成一个更大的有序数组。人们很快根据这个思路发明了一种简单的递归排序算法：归并排序。要将一个数组排序，可以先（递归地）将它分成两半分别排序，然后将结果归并起来。归并排序最吸引人的性质是它能保证任意长度为N的数组排序所需时间和NlogN成正比；它的主要缺点也显而易见就是它所需的额外空间和N成正比。简单的归并排序如下图：


![][2]
### 2，原理

　　归并（Merge）排序法是将两个（或两个以上）有序表合并成一个新的有序表，即把待排序序列分为若干个子序列，每个子序列是有序的。然后再把有序子序列合并为整体有序序列。
　　合并方法：
　　设r[i…n]由两个有序子表r[i…m]和r[m+1…n]组成，两个子表长度分别为n-i +1、n-m。

```
1、j=m+1；k=i；i=i; //置两个子表的起始下标及辅助数组的起始下标
2、若i>m 或j>n，转⑷ //其中一个子表已合并完，比较选取结束
3、//选取r[i]和r[j]较小的存入辅助数组rf
        如果r[i]<r[j]，rf[k]=r[i]； i++； k++； 转⑵
        否则，rf[k]=r[j]； j++； k++； 转⑵
4、//将尚未处理完的子表中元素存入rf
        如果i<=m，将r[i…m]存入rf[k…n] //前一子表非空
        如果j<=n ,  将r[j…n] 存入rf[k…n] //后一子表非空
5、合并结束。
```
### 3,实现代码

```java
/**
     * 归并排序 简介:将两个（或两个以上）有序表合并成一个新的有序表
     * 即把待排序序列分为若干个子序列，每个子序列是有序的。然后再把有序子序列合并为整体有序序列 时间复杂度为O(nlogn) 稳定排序方式
     * 
     * @param nums
     *            待排序数组
     * @return 输出有序数组
     */

    public static int[] mergeSort(int[] nums, int low, int high) {
        int mid = (low + high) / 2;
        if (low < high) {
            // 左边
            mergeSort(nums, low, mid);
            // 右边
            mergeSort(nums, mid + 1, high);
            // 左右归并
            merge(nums, low, mid, high);
        }
        return nums;
    }

    /**
     * 将数组中low到high位置的数进行排序
     * 
     * @param nums
     *            待排序数组
     * @param low
     *            待排的开始位置
     * @param mid
     *            待排中间位置
     * @param high
     *            待排结束位置
     */
    public static void merge(int[] nums, int low, int mid, int high) {
        int[] temp = new int[high - low + 1];
        int i = low;// 左指针
        int j = mid + 1;// 右指针
        int k = 0;

        // 把较小的数先移到新数组中
        while (i <= mid && j <= high) {
            if (nums[i] < nums[j]) {
                temp[k++] = nums[i++];
            } else {
                temp[k++] = nums[j++];
            }
        }

        // 把左边剩余的数移入数组
        while (i <= mid) {
            temp[k++] = nums[i++];
        }

        // 把右边边剩余的数移入数组
        while (j <= high) {
            temp[k++] = nums[j++];
        }

        // 把新数组中的数覆盖nums数组
        for (int k2 = 0; k2 < temp.length; k2++) {
            nums[k2 + low] = temp[k2];
        }
    }
```
## 第三章——进阶之快速排序
### 前言：

　　快速排序可能是应用最广泛的排序算法了。快速排序流行的原因主要因为它实现简单，适用于不同的输入数据且在一般应用中比其他排序算法都要快得多。快速排序引人注目的特点包括它是原地排序（只需要一个很小的辅助栈），且将长度为N的数组排序所需要的时间和NlgN成正比。我们之前提到的几种排序算法都无法将这两个优点结合起来。另外，快速排序的内循环比大多数排序算法都要短小，这意味着它无论是理论上还是实际中都要更快。它的主要缺点是非常脆弱，在实现时要非常小心才能避免低劣的性能。已经有无数例子显示许多错误都能致使它在实际应用中的性能只有平方级别。不过还好，我们由这些缺点和教训中大大改进了快速排序算法，使它的应用更加广泛。
### 1，介绍

　　快速排序是一种分治的排序算法。它将一个数组分成两个字数组，将两部分独立地排序。快速排序和归并排序是互补的：归并排序将数组分成两个字数组分别排序，并将有序的字数组归并以将整个数组排序；而快速排序将数组排序的方式则是当两个字数组都有序时整个数组也就自然有序了。在第一种情况中，递归调用发生在处理整个数组之前；在第二种情况中，递归调用发生在处理整个数组之后。在归并排序中，一个数组被等分为两半；快速排序中，切分的位置取决于数组的内容。快速排序的过程大致如下：


![][3]
### 2，原理
 **`快速排序的基本思想`** ：
　　通过一趟排序将待排序记录分割成独立的两部分，一部分全小于选取的参考值，另一部分全大于选取的参考值。这样分别对两部分排序之后顺序就可以排好了。
 **`例子：`** 
（a）一趟排序的过程：


![][4] 
（b）排序的全过程：


![][5]
### 3,实现代码

```java
    /**
     * 查找出中轴（默认是最低位low）的在numbers数组排序后所在位置
     * 
     * @param numbers 带查找数组
     * @param low 开始位置
     * @param high 结束位置
     * @return 中轴所在位置
     */
    public static int getMiddle(int[] numbers, int low, int high) {
        // 数组的第一个作为中轴
        int temp = numbers[low]; 
        while (low < high) {
            while (low < high && numbers[high] > temp) {
                high--;
            }
            // 比中轴小的记录移到低端
            numbers[low] = numbers[high];
            while (low < high && numbers[low] < temp) {
                low++;
            }
            // 比中轴大的记录移到高端
            numbers[high] = numbers[low]; 
        }
        numbers[low] = temp; // 中轴记录到尾
        return low; // 返回中轴的位置
    }

    /**
     * 
     * @param numbers 带排序数组
     * @param low 开始位置
     * @param high 结束位置
     */
    public static void quick(int[] numbers, int low, int high) {
        if (low < high) {
            int middle = getMiddle(numbers, low, high); // 将numbers数组进行一分为二
            quick(numbers, low, middle - 1); // 对低字段表进行递归排序
            quick(numbers, middle + 1, high); // 对高字段表进行递归排序
        }

    }

    /**
     * 快速排序
     * 快速排序提供方法调用
     * @param numbers 带排序数组
     */
    public static void quickSort(int[] numbers) {
        // 查看数组是否为空
        if (numbers.length > 0) 
        {
            quick(numbers, 0, numbers.length - 1);
        }
    }

```
### 4，改进方法

我们只介绍一种常用的，具体代码就不贴出了。想去的可以去[https://algs4.cs.princeton.ed...][7]　这个网站找。
 **`三向切分快速排序  `** ：
　　核心思想就是将待排序的数据分为三部分,左边都小于比较值,右边都大于比较值,中间的数和比较值相等.三向切分快速排序的特性就是遇到和比较值相同时,不进行数据交换,  这样对于有大量重复数据的排序时,三向切分快速排序算法就会优于普通快速排序算法,但由于它整体判断代码比普通快速排序多一点,所以对于常见的大量非重复数据,它并不能比普通快速排序多大多的优势 。
 **`欢迎关注我的微信公众号（分享各种Java学习资源，面试题，以及企业级Java实战项目回复关键字免费领取）：`** 


![][6]

[7]: https://algs4.cs.princeton.edu/code/
[0]: ./img/1460000013826616.png
[1]: ./img/1460000013826617.png
[2]: ./img/1460000013826618.png
[3]: ./img/1460000013826619.png
[4]: ./img/1460000013826620.png
[5]: ./img/1460000013826621.png
[6]: ./img/1460000013826622.png