## 排序算法

+ 冒泡排序

```JAVA 
public class BubbleSortTest{
    public static void main(Stirng[] args ){
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
		if(start<end){
		int stard =arrs[start];
		int low =start;
		int high =end;
		while(low<high){
			while(low<high&&stard<=arrs[high]){
				high--;
			}
			arrs[low] =arrs[high];
          //```````````````````````````````````````
			while(low<high&&arrs[low]<=stard){
				low++;
			}
			arrs[high]=arrs[low];
            
			arrs[low]=stard;
            
			quickSort(arrs,start,low);
			quickSort(arrs,low+1,end);
		}
		}
	}

}
```

