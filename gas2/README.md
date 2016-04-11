http://cs.mipt.ru/fileadmin/assembler/severov/2016/06-mashinnyi___uroven_3_Procedury.pdf

Переполнение стэка:

https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B1%D1%83%D1%84%D0%B5%D1%80%D0%B0

###Соглашене о вызове
Это часть двоичного интерфейса приложений (англ. application binary interface, ABI), которая регламентирует технические особенности вызова подпрограммы, передачи параметров, возврата из подпрограммы и передачи результата вычислений в точку вызова.

На разных системах может быть разной (особенно если сравнивать linux и windows)

1. Порядок, по которому выделяются регистры: Для целых: rdi, rsi, rdx, rcx, r8, r9. Для вещественных: (float, double), xmm0, xmm1, xmm2, xmm3, xmm4, xmm5, xmm6, xmm7
2. Дополнительные параметры (начиная с 7-го) помещаются в стек, и удаляются вызывающей функцией после вызова
3. После того как параметры засунуты в стек, сделан call , то адрес возврата лежит в  (%rsp), первый параметр памяти в  8(%rsp), и т.д.
4. Указатель стека %RSP должен быть выровнен по 16-байтной границе перед вызовом(call). Процесс вызова(сама комманда call) делает push адреса возврата (8 байт) в стек, поэтому, когда функция получает управление - %RSP не выровнен. Нужно сделать это самостоятельно через push или вычитания из 8 из %rsp.
5. Единственные регистры которые вызываемая функция должна сохранить это rbp, rbx, r12, r13, r14, r15. Остальные регистры могут быть изменены вызываемой функцией.
6. Целые возвращаются в rax или rdx:rax, вещественные в xmm0 или xmm1:xmm0 

Если мы передаем параметры меньше размера (например 32 бита), то регистр меняется на соответствующий (rdi на edi). См. таблицу ниже:

| 64-bit register | Lower 32 bits | Lower 16 bits | Lower 8 bits |
|-----------------|---------------|---------------|--------------|
| rax             | eax           | ax            | al           |
| rbx             | ebx           | bx            | bl           |
| rcx             | ecx           | cx            | cl           |
| rdx             | edx           | dx            | dl           |
| rsi             | esi           | si            | sil          |
| rdi             | edi           | di            | dil          |
| rbp             | ebp           | bp            | bpl          |
| rsp             | esp           | sp            | spl          |
| r8              | r8d           | r8w           | r8b          |
| r9              | r9d           | r9w           | r9b          |
| r10             | r10d          | r10w          | r10b         |
| r11             | r11d          | r11w          | r11b         |
| r12             | r12d          | r12w          | r12b         |
| r13             | r13d          | r13w          | r13b         |
| r14             | r14d          | r14w          | r14b         |
| r15             | r15d          | r15w          | r15b         |

Возрват происходит в rax(eax,ax,...)

Исследование стэка с помощью gdb

ftp://ftp.gnu.org/old-gnu/Manuals/gdb/html_chapter/gdb_7.html

Еще про стековый кадр и соглашение о вызове

http://eli.thegreenplace.net/2011/09/06/stack-frame-layout-on-x86-64/



Пример число из регистра
```asm

//увеличиваем число на 20, храним в rax
        .global main

        .text
main:

sss:
        mov     $20, %rax #ЭТО ЧИСЛО, КОТОРОЕ БУДЕТ ПЕЧАТАТЬСЯ

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


Печатаем число из секции .data
```asm

//увеличиваем число на 20, храним в rax
        .global main

        .text
main:

sss:
        mov     $format, %rdi           # set 1st parameter (format)
        mov     input, %rsi              # set 2nd parameter (current_number)
        xor     %rax, %rax              # because printf is varargs
        sub     $8, %rsp                # align stack pointer
        call    printf                  # printf(format, sum/count)
        add     $8, %rsp                # restore stack pointer

        ret

.data
input:   
        .quad 20 #ЭТО ЧИСЛО, КОТОРОЕ БУДЕТ ПЕЧАТАТЬСЯ
format:
        .asciz "%ld"

```


