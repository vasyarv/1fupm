#Системы счисления

Полезно просмотреть следующие слайды:

http://cs.mipt.ru/fileadmin/assembler/severov/2015/02-predstavlenie_dannykh_1.pdf

http://cs.mipt.ru/fileadmin/assembler/severov/2015/03-predstavlenie_dannykh_2.pdf

Очень полезно в некоторых задача вспомнить спецификацию printf:

d, i — десятичное знаковое число, размер по умолчанию, sizeof( int ). По умолчанию записывается с правым выравниванием, знак пишется только для отрицательных чисел. '%d' и '%i' ведут себя одинаково при выводе, но имеют разные значения при вводе с помощью функции scanf();

o — восьмеричное беззнаковое число, размер по умолчанию sizeof( int );

u — десятичное беззнаковое число, размер по умолчанию sizeof( int );

x и X — шестнадцатеричное число, x использует маленькие буквы (abcdef), X большие (ABCDEF), размер по умолчанию sizeof( int );

f и F — числа с плавающей запятой. По умолчанию выводятся с точностью 6, если число по модулю меньше единицы, перед десятичной точкой пишется 0. Величины ±∞ представляются в форме [-]inf или [-]infinity, Величина Nan представляется как [-]nan или [-]nan(любой текст далее). Использование F выводит указанные величины заглавными буквами (-INF, NAN). Аргумент по умолчанию имеет размер double.

e и E — числа с плавающей запятой в экспоненциальной форме записи (вида 1.1e+44); e выводит символ «e» в нижнем регистре, E — в верхнем (3.14E+0);

g и G — число с плавающей запятой; форма представления зависит от значения величины (f или e);

a и A — число с плавающей запятой в шестнадцатеричном виде;

c — вывод символа с кодом, соответствующим переданному аргументу; переданное число приводится к типу unsigned char (или wchar_t, если был указан модификатор длины l);

s — вывод строки с нулевым завершающим байтом; если модификатор длины — l, выводится строка wchar_t*. В Windows значения типа s зависят от типа используемых функций. Если используется семейство printf функций, то s обозначает строку char*. Если используется семейство wprintf функций, то s обозначает строку wchar_t*.

S — то же самое что и s с модификатором длины l; В Windows значения типа S зависит от типа используемых функций. Если используется семейство printf функций, то S обозначает строку wchar_t*. Если используется семейство wprintf функций, то S обозначает строку char*.

p — вывод указателя, внешний вид может существенно различаться в зависимости от внутреннего представления в компиляторе и платформе (например, 16 битная платформа MS-DOS использует форму записи вида FFEC:1003, 32-битная платформа с плоской адресацией использует адрес вида 00FA0030);

n — запись по указателю, переданному в качестве аргумента, количества символов, записанных на момент появления командной последовательности, содержащей n;

% — символ для вывода знака процента (%), используется для возможности вывода символов процента в строке printf, всегда используется в виде %%.
