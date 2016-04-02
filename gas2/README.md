Пример работы со scanf и printf (без использования стэка)
```asm

//увеличиваем число на 20, храним в rax
        .global main

        .text
main:

sss:
        mov     $format, %rdi           # set 1st parameter (format)
        mov     $input, %rsi              # set 2nd parameter (current_number)
        xor     %rax, %rax              # because printf is varargs
        sub     $8, %rsp                # align stack pointer
        call    scanf                  # printf(format, sum/count)
        add     $8, %rsp                # restore stack pointer

        mov     input, %rax


        add     $20, %rax

        
        mov     $format, %rdi           # set 1st parameter (format)
        mov     %rax, %rsi              # set 2nd parameter (current_number)
        xor     %rax, %rax              # because printf is varargs
        sub     $8, %rsp                # align stack pointer
        call    printf                  # printf(format, sum/count)
        add     $8, %rsp                # restore stack pointer

        ret

.data
input:   
        .quad 0x10  #если убрать 0x10 то будет некорректно работать
format:
        .asciz "%ld"

```

Версия с локальными переменными

```asm

//увеличиваем число на 20, храним в rax
        .global main

        .text
main:

sss:
        sub $8, %rsp      # allocate 8 bytes from stack
        mov $0, %rax      # clear rax
        mov $format, %rdi   # load format string
        mov %rsp, %rsi    # set storage to local variable

        call    scanf                  # printf(format, sum/count)
        mov     (%rsp), %rax
        add     $8, %rsp                # restore stack pointer


        add     $20, %rax

        
        mov     $format, %rdi           # set 1st parameter (format)
        mov     %rax, %rsi              # set 2nd parameter (current_number)
        xor     %rax, %rax              # because printf is varargs
        sub     $8, %rsp                # align stack pointer
        call    printf                  # printf(format, sum/count)
        add     $8, %rsp                # restore stack pointer

        ret

.data
format:
        .asciz "%ld"
```

