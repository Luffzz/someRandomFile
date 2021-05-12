# 操作系统课程设计 Project3

周轾 518030910189

[toc]

### Abstract

本次项目分两部分进行，首先编写了一个利用多线程进行排序的c程序，同时使用两个线程对整数列表的两个部分分别进行排序，并使用另一个线程合并完成排序的两个列表。其次，我利用java的fork函数以及join函数编写了快排和归并排序。

### 实现过程

直接使用gcc对编写完成的multiThreadSorting.c进行编译：Gcc multiThreadingSorting.c -lpthread -o multiThreadSorting在安装jdk后，使用javac quickSort.java, javac mergeSort.java进行编译。

### 代码编写

#### Multithreaded Sorting Application

为了实现每个线程中对子数组的排序，我定义了一个sort函数以完成选择排序，因为这种算法比较方便实现，同时定义了一个全局变量array以存储待排序的数组，以及一个全局变量final_array以存储最后的排序结果,其代码如下：

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

int *array;
int *final_array;
int array_length;
int middle;

void *insertionSort(void *arg){
    int *s = arg;
    int left = *s, right;
    //确定是对数组的前半部分还是后半部分排序
    if(*s == middle)
        right = array_length;
    else
        right = middle;
    //每次循环把最小的放在最左边
    for(int i=left; i<right; i++){
        for(int j=i+1; j<right; j++){
            if(array[j] < array[i]){
                int tmp = array[j];
                array[j] = array[i];
                array[i] = tmp;
            }
        }
    }
}
```

同时，还需要定义一个用于合并两个子数组的的mergeArray函数，其代码如下：

```c
void *mergeArray(void *arg){
	int current1 = 0;
    int current2 = middle;
  	int current_position = 0;
    while(current1 < middle && current2 < array_length){
        if(a[current1] < a[current2])
        {
            result_array[current_position] = a[current1];
            current1++;
            current_position++;
        }
        else{
            result_array[current_position] = a[current2];
            current2++;
            current_position++;
        }
    }
    //判断是哪一部分还剩下没有处理
    if(current1 == middle){
        while(current2<array_length){
            result_array[current_position] = a[current2];
            current_position++;
            current2++;
        }
    }
   	else{
        while(current1<middle){
            result_array[current_position] = a[current1];
            current_position++;
            current1++;
        }
    }
}
```

最后需要定义一个主函数以创建线程并对数组进行排序，使用pthread_create，pthread_join函数创建线程并开始执行，主要代码如下：

```c
int main(int argc, char *argv[]){
    
}
```

