# **Chapter 17 포인터의 포인터**

> ## 17-1 포인터의 포인터에 대한 이해
* **포인터의 포인터** (**'이중 포인터'** 또는 **'더블 포인터'**)  
: 포인터 변수를 가리키는 또 다른 포인터 변수  
 &nbsp; `int **dptr;    // int형 이중 포인터`

 <br>

 **포인터 변수를 가리키는 이중 포인터 변수 (더블 포인터 변수)**  
 ```c
 #include <stdio.h>

 int main(void)
 {
     double num = 3.14;
     double **ptr = &num;     // 변수 num의 주소값 저장
     double **dptr = &ptr;    // 포인터 변수 ptr의 주소값 저장
     double *ptr2;

     printf("%9p %9p \n", ptr, *dptr);     // *dptr은 ptr을 의미하므로 출력결과 동일
     printf("%9g %9g \n", num, **dptr);    // **dptr은 num을 의미하므로 출력결과 동일
     
     ptr2 = *dptr;     // ptr2 = ptr 과 같은 문장. 따라서 ptr2도 변수 num을 가리킴
     *ptr2 = 10.99;    // 변수 num의 값을 10.99로 변경
     
     printf("%9g %9g \n", num, **dptr);

     return 0;
 }
 ```
 ```
 [실행결과]
 0032FD00    0032FD00
     3.14        3.14
    10.99       10.99
```

* 포인터 변수의 참조관계  
    ![포인터의 참조관계](./Image/Chapter_17_1.png)  
    * 이 상황에서 변수 num에 접근하는 방법  
    \- &nbsp; `**dptr = 10.1;` &nbsp; &nbsp; &nbsp; &nbsp; 변수 num에 10.1 저장  
    \- &nbsp; `*ptr = 20.2;` &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 변수 num에 20.2 저장  
    \- &nbsp; `*ptr2 = 30.3;` &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 변수 num에 30.3 저장  
    \- &nbsp; `num = 40.4;` &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 변수 num에 접근하는 가장 기본적인 방법  

<br>

**포인터 변수 대상의 Call-by-reference**

[잘못된 코드]
```c
#include <stdio.h>

void SwapIntPtr(int *p1, int *p2)
{
    int *temp = p1;
    p1 = p2;
    p2 = temp;
}

int main(void)
{
    int num1 = 10, num2 = 20;
    int *ptr1 = &num1, *ptr2 = &num2;
    printf("*ptr1  *ptr2 : %d  %d \n", *ptr1, *ptr2);

    SwapIntPtr(ptr1, ptr2);
    printf("*ptr1  *ptr2 : %d  %d \n", *ptr1, *ptr2);
}
```
```
[실행결과]
*ptr1  *ptr2 : 10  20
*ptr1  *ptr2 : 10  20
```

* 포인터 변수의 참조관계를 바꿔서 함수 실행 결과 '20  10'이 출력되기를 원했지만 바뀌지 않음  
* 이유: `SwapIntPtr(ptr1, ptr2);` 의 결과 매개변수에 값만 전달됨 <br> &nbsp; &nbsp; &nbsp; ∴ p1과 p2에 저장된 값은 바뀌지만, 이는 ptr1과 ptr2와는 별개의 변수이기 때문에 <br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;ptr1은 여전히 num1의 주소값을, ptr2는 여전히 num2의 주소값을 저장하고 있는 상태  
    ![잘못된 코드 실행 과정 (1)](./Image/Chapter_17_2.png)
    ![잘못된 코드 실행 과정 (2)](./Image/Chapter_17_3.png)  
    * ptr1과 ptr2에 저장된 값은 서로 바뀌지 않음
* 함수 내에서 ptr1과 ptr2가 가리키는 대상을 바꿀 수 있는 방법?  
: 함수 내에서 변수 ptr1과 ptr2에 직접 접근이 가능해야 함! (→ 이중포인터 사용)

\[ 올바른 코드 \]

```c
#include <stdio.h>

/* 포인터 변수에 저장된 값의 변경이 목적이므로 포인터 변수의 주소값을 함수에 전달해야 함 */
void SwapIntPtr(int **dp1, int **dp2)
{
    int *temp = *dp1;    // int *temp = ptr1; 와 동일
    *dp1 = *dp2;         // ptr1 = ptr2; 와 동일
    *dp2 = temp;         // ptr2 = temp; 와 동일
}

int main(void)
{
    int num1 = 10, num2 = 20;
    int *ptr1 = &num1, *ptr2 = &num2;
    printf("*ptr1  *ptr2 : %d  %d \n", *ptr1, *ptr2);

    SwapIntPtr(&ptr1, &ptr2);    // ptr1과 ptr2의 주소값 전달
    printf("*ptr1  *ptr2 : %d  %d \n", *ptr1, *ptr2);
}
```
```
[실행결과]
*ptr1  *ptr2 : 10  20
*ptr1  *ptr2 : 20  10
```
* 실행 과정  
    ![올바른 코드 실행 과정](./Image/Chapter_17_4.png)

<br>

**포인터 배열과 포인터 배열의 포인터 형**

