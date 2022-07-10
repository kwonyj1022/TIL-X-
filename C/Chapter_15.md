# **Chapter 15 도전! 프로그래밍!**

도전 1 &nbsp; (입력한 정수 홀수 / 짝수 구분)

```c
#include <stdio.h>

void odd(int arr[])
{
    int i=0;
    printf("홀수 출력: ");

    for(i=0; i<10; i++)
    {
        if(arr[i] % 2 == 1)
        {
            printf("%d", arr[i]);
            if(i != 9)
                printf(", ");
        }
    }
    printf("\n");
}

void even(int arr[])
{
    int i=0;
    printf("짝수 출력: ");

    for(i=0; i<10; i++)
    {
        if(arr[i] % 2 == 0)
        {
            printf("%d ", arr[i]);
            if(i != 9)
                printf(", ");
        }
    }    
    printf("\n");
}

int main(void)
{
    int nums[10] = {0};
    int i=0;

    printf("총 10개의 숫자 입력 \n");
    for(i=0; i<10; i++)
    {
        printf("입력: ");
        scanf("%d", &nums[i]);
    }
    
    odd(nums);
    even(nums);

    return 0;
}
```

<br>

도전 2 &nbsp; (10진수 -> 2진수)

```c
#include <stdio.h>

int main(void)
{
    int num = 0;
    int bin[30] = {0};
    int i = 0;
    printf("10진수 정수 입력: ");
    scanf_s("%d", &num);
    
    for (i=0; ; i++)
    {
        if (num == 0)
        {
            printf("0000\n");
            return 0;
        }
        else if (num == 1)
        {
            printf("0001\n");
            return 0;
        }
        else
        {
            bin[i] = num % 2;
            num /= 2;
            if (num == 1)
            {
                bin[++i] = 1;
                break;
            }
        }
    }

    printf("2진수:");
    i = 4*(i/4 + 1) - 1;
    for (; i>=0; i--)
    {
        if (i%4 == 3)
            printf(" ");
        printf("%d", bin[i]);
    }

    return 0;
}
```

<br>

도전 3 &nbsp; (홀수는 앞에서부터, 짝수는 뒤에서부터 채워나가는 형식)
```c
#include <stdio.h>

int main(void)
{
    int input[10] = {0}, ouput[10] = {0};
    int i = 0, k = 0, j = 9;
    printf("총 10개의 숫자 입력 \n");
    for (i=0; i<10; i++)
    {
        printf("입력: ");
        scanf("%d", &input[i]);

        if (input[i] % 2 == 1)
            ouput[k++] = input[i];
        else
            ouput[j--] = input[i];
    }

    printf("배열 요소의 출력 : ");
    for (i=0; i<10; i++)
        printf("%d ", ouput[i]);
    
    return 0;
}
```

<br>

도전 4 &nbsp; (회문 판단)

```c
#include <stdio.h>

int wordlen(char word[])
{
    int i = 0;
    for (i=0; ; i++)
        if (word[i] == '/0')
            return i;
}

int judge(char word[])
{
    int i = 0;
    int l = wordlen(word) - 1;
    for (i=0; i <= l/2; i++)
    {
        if (word[i] == word[l - i])
            continue;
        else
            return 0;
    }
    return 1;
}

int main(void)
{
    char word[10];
    printf("문자열 입력: ");
    scanf("%s", word);
    int j = judge(word);
    if (j == 1)
        printf("회문입니다 \n");
    else
        printf("회문이 아닙니다 \n");
    
    return 0;
}
```

<br>

도전 5 &nbsp; (내림차순 정렬)
```c
#include <stdio.h>

void DesSort(int arr[], int len)
{
    int temp, i, j;
    for (i=0; i < len-1; i++)
    {
        for (j=0; j < len-i-1; j++)
        {
            if (arr[j+1] > arr[j])
            {
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

int main(void)
{
    int arr[7] = {0};
    int i = 0;
    for (i=0; i<7; i++)
    {
        printf("입력: ");
        scanf_s("%d", &arr[i]);
    }

    DesSort(array, 7);

    for (i=0; i<7; i++)
        printf("%d", arr[i]);
    
    printf("\n");

    return 0;
}
```

<br>
<br>
<br>
<br>
<br>
출처: 윤성우의 열혈 C 프로그래밍
