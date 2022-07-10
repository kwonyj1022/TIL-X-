# **Chapter 10 도전! 프로그래밍!**

도전 1 &nbsp; (10진수 입력 --> 16진수 출력)

```c
#include <stdio.h>

int main(void)
{
    int num;
    printf("정수 입력: ");
    scanf("%d", &num);
    printf("16진수로: %x", num);
    return 0;
}
```

<br>

도전 2 &nbsp; (두 수 사이의 구구단 출력)

```c
#include <stdio.h>

void googoodan(int a, int b)
{
    int i, dan;

    if (a < b)
    {
        for (dan = a; dan <= b; dan++)
        {
            printf("\n-------- %d단 --------\n", dan);
            for (i = 1; i <= 9; i++)
                printf("%d * %d = %d \n", dan, i, dan * i);
        }
    }
    else
    {
        for (dan = b; dan <= a; dan++)
        {
            printf("\n-------- %d단 --------\n", dan);
            for (i = 1; i <= 9; i++)
                printf("%d * %d = %d \n", dan, i, dan * i);
        }
    }
}

int main(void)
{
    int a, b;
    printf("정수 2개 입력: ");
    scanf("%d %d", &a, &b);
    googoodan(a, b);
    return 0;
}
```

<br>

도전 3 &nbsp; (최대공약수 구하기)

```c
#include <stdio.h>

int main(void)
{
    int a, b;
    int i;
    
    printf("정수 2개 입력: ");
    scanf("%d %d", &a, &b);
    
    if (a > b)
    {
        for (i = a; i > 0; i--)
            if (a % i == 0 & b % i == 0)
                break;
    }
    else
    {
        for (i = b; i > 0; i--)
            if (a % i == 0 & b % i == 0)
                break;
    }
    
    printf("%d와 %d의 최대공약수: %d \n", a, b, i);
    
    return 0;
}
```

<br>

도전 4 &nbsp; (물건 구매의 경우의 수)

```c
#include <stdio.h>

int main(void)
{
    int bread, snack, coke;
    
    printf("현재 당신이 소유하고 있는 금액: 3500 \n");
    
    for (bread = 7; bread > 0; bread--)
        for (snack = 5; snack > 0; snack--)
            for (coke = 8; coke > 0; coke--)
                if (bread * 500 + snack * 700 + coke * 400 == 3500)
                    printf("크림빵 %d개, 새우깡 %d개, 콜라 %d개 \n", bread, snack, coke);
                    
    printf("어떻게 구입하시겠습니까? \n");
    
    return 0;
}
```

<br>

도전 5 &nbsp; (10개의 소수 출력)

```c
#include <stdio.h>

int sosu(int num)    // 소수면 0, 소수가 아니면 1을 반환하는 함수 정의
{
    if (num == 2)    // 2는 소수이므로 전달값이 2면 무조건 0 반환
        return 0;
    else
    {
        int i;
        int b = 0;                   // b = 0이고, 소수가 아닌 것으로 판명나면 b = 1이 됨
        for (i = 2; i < num; i++)    // 2이상 전달값 이하의 수로 나눠서 나누어떨어지면 소수 아님
        {
            if (num % i == 0)    // 1과 자기자신 이외의 수로 나누어 떨어지면 b = 1이 되고 반복문 탈출
            {
                b = 1;
                break;
            }
            else
                continue;
        }

        if (b == 0)    // b = 0이면 소수이고 b = 1이면 소수 아님
            return 0;
        else
            return 1;

    }
}

int main(void)
{
    int num;
    int b = 0;
    for (num = 2; num < 100; num++)    // 2 이상의 수를 함수 sosu에 전달
        if (sosu(num) == 0)    // sosu 함수의 반환값이 0이면, 즉 전달인자가 소수이면 b가 1씩 증가
        {
            b += 1;
            if (b <= 5)        // b <= 5이면 num 출력 (소수 5개 출력해야 하므로)
                printf("%d \n", num);
            else
                break;
        }
    return 0;
}
```

<br>

도전 6 &nbsp; (초 &nbsp; --> &nbsp; 시, 분, 초)

```c
#include <stdio.h>

int main(void)
{
    int second;
    int h, m, s;
    printf("초(second) 입력: ");
    scanf("%d", &second);
    
    h = second / 3600;
    m = (second % 3600) / 60;
    s = second % 60;
    
    printf("[h: %d, m: %d, s: %d]", h, m, s);
    
    return 0;
}
```

<br>

도전 7 &nbsp; (2^k <= n을 만족하는 k의 최댓값)

```c
#include <stdio.h>
int jagob(int k)
{
    int i;
    int value = 1;
    for (i = 0; i < k; i++)
        value = value * 2;
    return value;
}

int main(void)
{
    int n, k;
    printf("상수 n 입력: ");
    scanf("%d", &n);
    
    for (k = 1; k > 0; k++)
        if (jagob(k) > n)
            break;
            
    printf("공식을 만족하는 k의 최댓값은 %d \n", k-1);
    
    return 0;
}
```

<br>

도전 8 &nbsp; (2의 n승을 구하는 재귀함수)

```c
#include <stdio.h>

int seung(int n)
{
    if (n == 0)
        return 1;
    else
        return 2 * seung(n-1);
}

int main(void)
{
    int n;
    printf("정수 입력: ");
    scanf("%d", &n);
    printf("2의 %d승은 %d", n, seung(n));
    return 0;
}
```

<br>
<br>
<br>
<br>
<br>
출처: 윤성우의 열혈 C 프로그래밍
