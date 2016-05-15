## Связывание, make файлы

```c
int sum(int a,int b);

int main() {
        int result = sum(1,2);
        return result*2;

}
```

```c
int sum(int a, int b) {
        return a + b;
}
```

```bach
gcc -o program main.c sum.c
./program; echo $?
```

Получим промежуточные объектные файлы
```bash
gcc -c main.c
gcc -c sum.c
gcc -o program main.o sum.o
```

`objdump -d -r main.o`

R_386_PC32 - релокация, если будем использовать эту функцию, то нужно где-то её взять.


`readelf -s main.o` - секция .text

`readelf -t main.o` - список секций

`objdump -d -r program`

После сборки.

        1. Вставилась функция sum, почти не изменившись и получила конкретный адрес
        2. Функция sum вызывается в main по адресу


посмотрим заголовки

`readelf -h main.o` - Relocatable file, entry point 0 - значит запустить нельзя

`readelf -h program` - Exec file , entry point != 0

Чтобы не писать объявление можно вынести его в заголовочный файл
```c
include sum.h
```

```c
int sum(int a,int b);
```

`gcc -E main.c` - соберет все файлы в один

Препроцессор просто совершает текстовые подстановки и ничего больше не делает.

Какие мы помним директивы препроцессора?

Процесс:

Препроцессинг(один файл с кодом) - Компиляция(объектные файлы) - Сборка(исполняемый файл)

include <> "" определяет лишь в каких директориях мы сначала ищем


man makefile

http://mrbook.org/blog/tutorials/make/

https://habrahabr.ru/post/155201/
