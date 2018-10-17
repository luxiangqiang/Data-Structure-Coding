```c
#include<stdio.h>
int main()
{
	//声明函数
	int array_border();
	
	//调用函数	
	array_border();
	return 0;
}

//数组越界检测
int array_border(){
    int i = 0;
    int arr[3] = {0};
    for(; i<=3; i++){
        arr[i] = 0;
        printf("hello world\n");
    }
    return 0;
}

//代码运行结果
//出现无限循环打印 hello world
```

