Лекция:
http://cs.mipt.ru/fileadmin/assembler/severov/2016/04-mashinnyi___uroven_1_Osnovy.pdf

Команды:
http://www.jegerlehner.ch/intel/IntelCodeTable.pdf

Статья про отличие синтаксиса:

https://ru.wikipedia.org/wiki/AT%26T-%D1%81%D0%B8%D0%BD%D1%82%D0%B0%D0%BA%D1%81%D0%B8%D1%81

###Ассемблерная вставка (Intel)

```c
#include <stdio.h>
int a,b;
int main()
{
    scanf("%d",&a);
    asm volatile(
        ".intel_syntax noprefix;\n"
        "mov  eax, a\n"
        /* и другой ассемблерный код, который заключен в ", оканчивается на \n */
        "mov a, eax\n"
        ".att_syntax noprefix;"
    );
    printf("%d\n",a);
    return 0;
}
```

###Ассемблерная вставка (AT&T)
```c
#include <stdio.h>
int a,b;
int main()
{
    scanf("%d",&a);
    asm volatile(
        "movl a, %eax\n"
        /* и другой ассемблерный код, который заключен в ", оканчивается на \n */
        "movl %eax, a\n"
        ".att_syntax noprefix;"
    );
    printf("%d\n",a);
    return 0;
}
```
