Лекции Северова:

http://cs.mipt.ru/fileadmin/assembler/severov/2016/04-mashinnyi___uroven_1_Osnovy.pdf

http://cs.mipt.ru/fileadmin/assembler/severov/2016/05-mashinnyi___uroven_2_Upravlenie.pdf

Полезная книга:

https://ru.wikibooks.org/wiki/%D0%90%D1%81%D1%81%D0%B5%D0%BC%D0%B1%D0%BB%D0%B5%D1%80_%D0%B2_Linux_%D0%B4%D0%BB%D1%8F_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%81%D1%82%D0%BE%D0%B2_C

Скомпилируем код в ассемблер:

```c
long plus(long x, long y) {
	return x + y;
}
void sumstore(long x, long y,long *dest) {
	long t = plus(x, y);
	*dest = t;
}

int main() {
	return 0;
} 
```
Команда компиляции: `gcc -Og -S sum.c`

Далее скомпилируем этот код в обычный файл, и сделаем objdump:

```bash
gcc sum.c
objdump -d a.out
```

