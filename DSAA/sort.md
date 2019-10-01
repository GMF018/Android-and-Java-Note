

## 排序算法

+ 冒泡排序


```JAVA 
public class BubbleSortTest{
    public static void main(String[] args ){
      int[] sorts ={1,10,15,18,3};
		bubbleSort(sorts);
		for(int i:sorts){
			System.out.print(i+"\t");
		}
    }
	public static void bubbleSort(int[] arr){
	    if(arr==null){
	        return;
	    }
	    for(int i=0;i<arr.length-1;i++){//总共多少轮
	        for(int j=0;j<arr.length-1-i;j++){//每一轮的次数
	            if(arr[j]>arr[j+1]){
	                int temp=arr[j];
	                arr[j] =arr[j+1];
	                arr[j+1]=temp;
	            }
	        }
	    }
}
输入：1 3 10 15 18  
```
+ 快速排序

```java
public class QuickSort {
		
	public static void main(String[] args) {
		int[] arrs ={1,6,3,7,8,0,1,2,83,7,9};
		quickSort(arrs,0,arrs.length-1);
		System.out.print(Arrays.toString(arrs));
		
	}
    //双指针模式--》从高位开始比较，如果比标准数小就将当前指针下的数赋值到低位
    //然后从低位指针开始
    public static void quickSort(int[]arrs,int start,int end){
        //把数组中的第0个数值作为标准值，（拿出来，让左边有空位）
        int stard =arrs[start];
        //记录需要排序的下标
        int low =start;
        int high =end;
        if(start<end){
            //循环找出比标准数大和比标准数小的数
            while(low<high){
                //右指针开始读数
                while(low<high&&stard<=arrs[high]){//右边的数字比标准数大
                    high--;//指针左移
                }
                //使用右边的数字替换左边的数
                arrs[low] =arrs[high];
                //指针切换
                //做指针开始读数
                while(low<high&&arrs[low]<=stard){//左边的数字比标准数小
                    low++;//指针右移
                }
                //使用左边的数字替换右边的数
                arrs[high]=arrs[low];
            }
            //填补空位
            arrs[low]=stard;
            quickSort(arrs,start,low);
            quickSort(arrs,low+1,end);
        }
    }
```

+ 插入排序
  + 在前面已经排好序的序列中找到合适的插入位置
  + 步骤：

    1. 从第一个元素开始，该元素可以认为已经排好序。

    2. 取出下一个元素，在已经排好序的元素序列中从后往前扫描进行比较。

    3. 如果该元素(已排序) 大于新元素，则将该元素移到下一位置。

    4. 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置。

    5. 将新元素插入到该位置后面。


```java 
public class InsertSortTest {
    public static void main(String[] args) {
        int[] sorts = {1, 10, 15, 18, 3, 1, 32, 5215, 1361, 367, 47};
        insertSort(sorts);
        System.out.println(Arrays.toString(sorts));
    }

    private static void insertSort(int[] sorts) {
        if (sorts == null || sorts.length == 0) {
            return;
        }
        //遍历所有的数字
        for (int i = 1; i < sorts.length; i++) {
            if (sorts[i] < sorts[i - 1]) {
                //存储当前遍历的数字
                int temp = sorts[i];
                int j;
                //遍历当前数字前面的所有的数字
                for (j = i - 1; j >= 0 && temp < sorts[j]; j--) {//如果存储的数字比当前所有数字的最高位小，那么就将最高位的数字与当前的i（即j+1）调换
                    //也就是将前一个数字赋给后一个数字
                    sorts[j + 1] = sorts[j];
                }
                //临时变量（外层for循环的当前元素）赋给不满足条件的后一个元素
                sorts[j + 1] = temp;
            }
        }
    }
}
```

+ 希尔排序（遇到大小不一致的，比插入排序效率高）
+ 选择排序【简单排序】

```java 
public class SimpleSelectSortTest {
    public static void main(String[] args) {
        int[] sorts = {1, 10, 15, 18, 3, 1, 32, 5215, 1361, 367, 47};
        simpleSelectSort(sorts);
        System.out.println(Arrays.toString(sorts));
    }

    private static void simpleSelectSort(int[] sorts) {//每轮都找出最小的数
        for (int i = 0; i < sorts.length; i++) {
            for (int j = i + 1; j < sorts.length; j++) {
                if (sorts[j] < sorts[i]) {
                    int temp = sorts[j];
                    sorts[j] = sorts[i];
                    sorts[i] =temp;
                }
            }
        }
    }
}
```



+ 归并排序
+ 基数排序

| 类型     | 时间复杂度 | 空间复杂度 | 稳定性 |
| -------- | ---------- | ---------- | ------ |
| 冒泡排序 | O(n^2)     | O(1)       | 稳定   |
| 快速排序 |            |            |        |
| 插入排序 |            |            |        |
| 希尔排序 |            |            |        |
| 选择排序 |            |            |        |
| 基数排序 |            |            |        |
| 堆排序   |            |            |        |

最差时间分析	平均时间复杂度	稳定度	空间复杂度
冒泡排序	O(n2)	O(n2)	稳定	O(1)
快速排序	O(n2)	O(n*log2n)	不稳定	O(log2n)~O(n)
选择排序	O(n2)	O(n2)	稳定	O(1)
二叉树排序	O(n2)	O(n*log2n)	不一顶	O(n)
插入排序

O(n2)	O(n2)	稳定	O(1)
堆排序	O(n*log2n)	O(n*log2n)	不稳定	O(1)
希尔排序	O	O	不稳定	O(1)
————————————————



