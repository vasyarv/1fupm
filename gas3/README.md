##Инструкции с вещественными числами

Хорошая статья, где есть разные примеры и не только на вещественные числа: http://cs.lmu.edu/~ray/notes/gasexamples/

https://ru.wikipedia.org/wiki/SSE

Для вещественных операций используются 8(16) регистров xmm0,xmm1, ...

Пример scanf:

```asm
        sub     $8, %rsp        # сдвигаем стэк, попутно аллоцируем 8 байт (сколько это бит?)
        mov     $0, %rax        # кол-во вещественнозначных аргументов - 0. Принимаем адрес
        mov     $format, %rdi   # просто загрузили формат строки
        mov     %rsp, %rsi      # сюда будем записывать
        call    scanf           # дергаем функцию
        add     $8, %rsp        # восстанавливаем указатель стека
        
        movsd   (%rsp), %xmm0   # а вот темерь в xmm0 лежит наше число
```

А теперь пример printf?

```asm
        mov     $format, %rdi           # set 1st parameter (format)
        mov     $1, %rax                # because printf is varargs
        sub     $8, %rsp                # align stack pointer
        call    printf                  # printf(format, sum/count)
        add     $8, %rsp                # restore stack pointer
```

Что напечает?

Про функции с переменным числом аргументов: http://learnc.info/c/vararg_functions.html

Печать целого числа из глобальных переменных:

```asm
.text
        ...
        cvtsi2sd   num, %xmm0           #наше число сконвертировали в double и положили в регистр xmm0
        mov     $format, %rdi           # формат
        mov     $1, %rax              # 1 вещественный регистр
        sub     $8, %rsp                
        call    printf                  
        add     $8, %rsp                # restore stack pointer
        ...
        ...
.data
format:
        .asciz "%lf"    #%lf - для double, %f - для float
num:   
        .octa 3 #наше число
```