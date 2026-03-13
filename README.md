Язык который можно и нужно улучшать под себя и тд , джанный язык не мой это реконстркция из непроверенных источников якобы они создали Xerox PARC но это не точно сам язык мертв а данных особо не было о нем но это так чисто есть значит есть нету значит вот появился.
Если язык был то к нему отношение не имею только реконстрктивное отношение, если не было то тогда полная моя работа по воссоздании из разных источников полная Mit lisense типо берете делаете че хотите мне пофиг это наоборот хороший пример работы с жжелезом прям нормально.
A language that can and should be improved to suit your needs, etc. The C+ language is not mine; it is a reconstruction based on unverified sources, claiming that they created Xerox PARC. However, it is uncertain whether the language itself is dead, and there is limited information about it. Nevertheless, it is a fact that the language exists.
If the language existed, I have no involvement with it other than the reconstruction. If it did not exist, then my full effort was to recreate it from various sources. This is a good example of working with hardware.
---

#Rus version(Русский)


# ПОЛНЫЙ СПРАВОЧНИК ЯЗЫКА C+
## Версия 1.0 (1974)

---

## ЧАСТЬ 1: ОБЩАЯ ИНФОРМАЦИЯ

### 1.1 Философия языка

C+ создавался как графическое расширение языка C. Основные принципы:

| Принцип | Описание |
|:--------|:---------|
| **Прямой доступ к железу** | Минимум абстракций между кодом и графическим аппаратным обеспечением |
| **Упрощение графики** | Синтаксис, интуитивно понятный для работы с пикселями и экраном |
| **Экспериментальные типы** | Новые типы данных для работы с графическими объектами |
| **Наследие B** | Сохранение простоты и эффективности языка B/раннего C |

### 1.2 Целевая платформа

| Характеристика | Значение |
|:---------------|:---------|
| **Процессор** | 16-битный микропрограммируемый ЦП |
| **Память** | 128-512 КБ |
| **Дисплей** | 606 x 808 пикселей (портретный режим), монохромный |
| **Устройства ввода** | Клавиатура + трёхкнопочная мышь |
| **Сеть** | Ethernet |

---

## ЧАСТЬ 2: ЛЕКСИКА И СИНТАКСИС

### 2.1 Набор символов

```
Буквы:        A-Z a-z _
Цифры:        0-9
Спецсимволы:  + - * / = ! < > & | ^ ^ % . , ; : ? ' " ( ) [ ] { } #
Пробельные:   пробел, табуляция, перевод строки
```

### 2.2 Ключевые слова

```
auto        array       bit        break       case        char
clear       color       continue    default     display     do
draw        else        fill        for         goto        if
int         line        mouse       pixel       register    return
short       sizeof      struct      switch      typedef     unsigned
void        wait        while       word
```

### 2.3 Комментарии

```c
// Однострочный комментарий

/* Многострочный
   комментарий */
```

### 2.4 Идентификаторы

- Длина: до 31 символа (первые 8 значимы для линкера)
- Регистрозависимость
- Начинаются с буквы или подчёркивания

---

## ЧАСТЬ 3: ТИПЫ ДАННЫХ

### 3.1 Базовые типы

| Тип | Размер | Диапазон | Описание |
|:----|:-------|:---------|:---------|
| `char` | 8 бит | -128..127 или 0..255 | Символ или малый integer |
| `short` | 16 бит | -32768..32767 | Короткое целое |
| `int` | 16 бит | -32768..32767 | Целое |
| `unsigned` | 16 бит | 0..65535 | Беззнаковое целое |
| `long` | 32 бит | -2^31..2^31-1 | Длинное целое |
| `float` | 32 бит | ~1e-38..1e38 | С плавающей точкой |
| `double` | 64 бит | ~1e-308..1e308 | Двойной точности |
| `void` | 0 | - | Пустой тип |

### 3.2 Специальные типы C+

| Тип | Размер | Описание | Пример |
|:----|:-------|:---------|:-------|
| `pixel` | 1 бит | Значение пикселя | `pixel p = 1;` |
| `color` | 24 бит | Экспериментальный цвет | `color red = #FF0000;` |
| `point` | 32 бит | Координаты (x,y) | `point p = {100,200};` |
| `rect` | 64 бит | Прямоугольник (x1,y1,x2,y2) | `rect r = {0,0,100,100};` |
| `mouse` | 32 бит | Позиция мыши + кнопки | `mouse m;` |
| `bitmap` | Переменный | Битовый массив | `bitmap icon[32x32];` |
| `word` | 16 бит | Машинное слово | `word* video = 0170000b;` |

### 3.3 Производные типы

| Тип | Синтаксис | Пример |
|:----|:----------|:-------|
| Указатель | `type*` | `int* ptr;` |
| Массив | `type[N]` | `int buf[100];` |
| Структура | `struct { ... }` | `struct point { int x; int y; };` |
| Объединение | `union { ... }` | `union { int i; char c; };` |
| Перечисление | `enum { ... }` | `enum bool { FALSE, TRUE };` |

### 3.4 Специальный синтаксис для массивов

```c
// Обычный C
int screen[606][808];
screen[100][200] = 1;

// C+ — упрощённый синтаксис
array screen[606x808];          // Двумерный массив одной декларацией
screen[100,200] = 1;            // Интуитивный доступ по координатам

// Другие варианты
array fb[640x480];                // Frame buffer
array icon[16x16];                // Иконка
array font[128x8];                 // Шрифт
```

---

## ЧАСТЬ 4: ПЕРЕМЕННЫЕ И ОБЪЯВЛЕНИЯ

### 4.1 Классы памяти

| Класс | Описание |
|:------|:---------|
| `auto` | Локальная переменная (по умолчанию) |
| `register` | Просьба хранить в регистре |
| `static` | Статическая переменная (сохраняет значение) |
| `extern` | Внешняя переменная (в другом файле) |

```c
auto int x = 10;           // Локальная переменная
register int counter;      // В регистре (для скорости)
static int global_count;   // Статическая
extern array screen[];     // Определена в другом месте
```

### 4.2 Инициализация

```c
int i = 100;
char c = 'A';
point origin = {0, 0};
rect screen_rect = {0, 0, 605, 807};
color white = #FFFFFF;

array fb[640x480] = {0};     // Весь массив нулями
```

### 4.3 Константы

```c
// Целые
int i = 1234;       // Десятичная
int o = 0123;       // Восьмеричная (начинается с 0)
int h = 0x1A3F;     // Шестнадцатеричная

// С плавающей точкой
float f = 3.14159;
double d = 2.7e-10;

// Символьные
char nl = '\n';     // Символ новой строки
char tab = '\t';    // Табуляция
char c = 'A';       // Обычный символ

// Строковые
char* msg = "Hello!";
```

### 4.4 Автоматический вывод типа

```c
auto x = 100;           // Тип int
auto y = 3.14;          // Тип float
auto p = &x;            // Тип int*
auto name = "C+";       // Тип char*
```

---

## ЧАСТЬ 5: ОПЕРАТОРЫ

### 5.1 Арифметические операторы

| Оператор | Значение | Пример |
|:---------|:---------|:-------|
| `+` | Сложение | `a + b` |
| `-` | Вычитание | `a - b` |
| `*` | Умножение | `a * b` |
| `/` | Деление | `a / b` |
| `%` | Остаток | `a % b` |
| `++` | Инкремент | `i++` или `++i` |
| `--` | Декремент | `i--` или `--i` |

### 5.2 Операторы сравнения

| Оператор | Значение | Пример |
|:---------|:---------|:-------|
| `==` | Равно | `a == b` |
| `!=` | Не равно | `a != b` |
| `<` | Меньше | `a < b` |
| `>` | Больше | `a > b` |
| `<=` | Меньше или равно | `a <= b` |
| `>=` | Больше или равно | `a >= b` |

### 5.3 Логические операторы

| Оператор | Значение | Пример |
|:---------|:---------|:-------|
| `&&` | Логическое И | `a && b` |
| `\|\|` | Логическое ИЛИ | `a \|\| b` |
| `!` | Логическое НЕ | `!a` |

### 5.4 Побитовые операторы

| Оператор | Значение | Пример |
|:---------|:---------|:-------|
| `&` | Побитовое И | `a & b` |
| `\|` | Побитовое ИЛИ | `a \| b` |
| `^` | Побитовое исключающее ИЛИ | `a ^ b` |
| `~` | Побитовое НЕ | `~a` |
| `<<` | Сдвиг влево | `a << 2` |
| `>>` | Сдвиг вправо | `a >> 2` |

### 5.5 Операторы присваивания

| Оператор | Эквивалент | Пример |
|:---------|:-----------|:-------|
| `=` | Простое | `a = b` |
| `+=` | `a = a + b` | `a += b` |
| `-=` | `a = a - b` | `a -= b` |
| `*=` | `a = a * b` | `a *= b` |
| `/=` | `a = a / b` | `a /= b` |
| `%=` | `a = a % b` | `a %= b` |
| `&=` | `a = a & b` | `a &= b` |
| `\|=` | `a = a \| b` | `a \|= b` |
| `^=` | `a = a ^ b` | `a ^= b` |
| `<<=` | `a = a << b` | `a <<= b` |
| `>>=` | `a = a >> b` | `a >>= b` |

### 5.6 Специальные операторы C+

| Оператор | Значение | Пример |
|:---------|:---------|:-------|
| `[x,y]` | Доступ к 2D-массиву | `screen[100,200]` |
| `@` | Взять адрес видеопамяти | `@display` |
| `#` | Цветовая константа | `#FF0000` |
| `::` | Доступ к системным регистрам | `video::mode` |

---

## ЧАСТЬ 6: УПРАВЛЯЮЩИЕ КОНСТРУКЦИИ

### 6.1 Условный оператор `if`

```c
if (condition) {
    // код
}

if (condition) {
    // код
} else {
    // другой код
}

if (x < 0) {
    x = 0;
} else if (x > max_x) {
    x = max_x;
} else {
    // нормальный случай
}
```

### 6.2 Оператор выбора `switch`

```c
switch (key) {
    case 'a':
    case 'A':
        move_left();
        break;
    case 'd':
    case 'D':
        move_right();
        break;
    default:
        beep();
        break;
}
```

### 6.3 Цикл `while`

```c
while (condition) {
    // тело цикла
}

// Бесконечный цикл
while (1) {
    handle_events();
}
```

### 6.4 Цикл `do-while`

```c
do {
    // выполнится хотя бы раз
} while (condition);
```

### 6.5 Цикл `for`

```c
for (init; condition; increment) {
    // тело
}

// Пример
for (i = 0; i < 640; i++) {
    screen[i,240] = 1;  // горизонтальная линия
}
```

### 6.6 Операторы перехода

| Оператор | Назначение |
|:---------|:-----------|
| `break;` | Выход из цикла или switch |
| `continue;` | Переход к следующей итерации |
| `goto label;` | Безусловный переход |
| `return;` | Возврат из функции |
| `return value;` | Возврат с значением |

---

## ЧАСТЬ 7: ФУНКЦИИ

### 7.1 Объявление функций

```c
// Возвращаемый тип  имя(параметры)
int add(int a, int b) {
    return a + b;
}

// Без возвращаемого значения
void clear_screen() {
    fill(screen, 0, 0, 605, 807, 0);
}

// С параметрами по умолчанию (эксперимент!)
void draw_point(int x, int y, int color = 1) {
    screen[x,y] = color;
}
```

### 7.2 Старый стиль (из B/раннего C)

```c
draw(x, y, color)
int x, y, color;  // параметры объявлены отдельно
{
    screen[x,y] = color;
}
```

### 7.3 Функции с переменным числом аргументов

```c
printf(format, ...)
char* format;
{
    // обработка переменных аргументов
}
```

---

## ЧАСТЬ 8: СТРУКТУРЫ И ОБЪЕДИНЕНИЯ

### 8.1 Определение структур

```c
// Простая структура
struct point {
    int x;
    int y;
};

// Структура с вложением
struct rectangle {
    struct point p1;
    struct point p2;
};

// Структура с битовыми полями
struct video_register {
    unsigned mode : 2;
    unsigned enable : 1;
    unsigned int : 5;  // пропуск 5 бит
    unsigned page : 8;
};
```

### 8.2 Использование структур

```c
// Объявление
struct point p;
struct rectangle r;

// Инициализация
struct point origin = {0, 0};
struct point cursor = {320, 240};

// Доступ к полям
p.x = 100;
p.y = 200;
x = p.x;

// Присваивание структур
p = origin;

// Указатели на структуры
struct point* ptr = &origin;
(*ptr).x = 50;
ptr->y = 60;  // оператор ->
```

### 8.3 Объединения

```c
union int_or_char {
    int i;
    char c[2];
};

union int_or_char u;
u.i = 0x4142;  // 'A' 'B'
char first = u.c[0];  // 'A'
```

---

## ЧАСТЬ 9: УКАЗАТЕЛИ И АДРЕСАЦИЯ

### 9.1 Основы указателей

```c
int x = 10;
int* ptr = &x;     // ptr указывает на x
int y = *ptr;      // y = 10

*ptr = 20;         // x теперь 20
```

### 9.2 Арифметика указателей

```c
int arr[10];
int* p = arr;      // указывает на arr[0]
p++;               // теперь на arr[1]
int* q = arr + 5;  // указывает на arr[5]
```

### 9.3 Указатели на видеопамять

```c
// Прямой доступ к видеопамяти
word* video_mem = (word*)0170000b;

// Работа с памятью как с массивом
video_mem[1000] = 0xFFFF;  // зажечь 16 пикселей

// Через специальный синтаксис C+
word* fb = @display;        // взять адрес дисплея
```

### 9.4 Указатели на функции

```c
// Определение типа указателя на функцию
void (*handler)(int, int);

// Присваивание
handler = draw_point;

// Вызов
handler(100, 200);
```

---

## ЧАСТЬ 10: ПРЕПРОЦЕССОР

### 10.1 Директивы препроцессора

| Директива | Назначение | Пример |
|:----------|:-----------|:-------|
| `#define` | Макроопределение | `#define WIDTH 640` |
| `#undef` | Отмена макроса | `#undef WIDTH` |
| `#include` | Вставка файла | `#include "graphics.h"` |
| `#ifdef` | Если определён | `#ifdef DEBUG` |
| `#ifndef` | Если не определён | `#ifndef HEADER_H` |
| `#if` | Условная компиляция | `#if WIDTH > 600` |
| `#else` | Иначе | `#else` |
| `#elif` | Иначе если | `#elif WIDTH == 640` |
| `#endif` | Конец условия | `#endif` |
| `#line` | Изменить номер строки | `#line 100 "file.c"` |
| `#error` | Сообщение об ошибке | `#error "Version mismatch"` |
| `#pragma` | Инструкция компилятору | `#pragma optimize` |

### 10.2 Примеры макросов

```c
// Константы
#define SCREEN_WIDTH  606
#define SCREEN_HEIGHT 808
#define WHITE 1
#define BLACK 0

// Макросы с параметрами
#define MIN(a,b) ((a) < (b) ? (a) : (b))
#define MAX(a,b) ((a) > (b) ? (a) : (b))
#define ABS(x) ((x) < 0 ? -(x) : (x))

// Графические макросы
#define SETPIXEL(arr,x,y,val) (arr[x,y] = (val))
#define GETPIXEL(arr,x,y) (arr[x,y])
```

### 10.3 Предопределённые макросы

| Макрос | Значение |
|:-------|:---------|
| `__LINE__` | Текущая строка |
| `__FILE__` | Текущий файл |
| `__DATE__` | Дата компиляции |
| `__TIME__` | Время компиляции |
| `__C_PLUS__` | Всегда определён для C+ |

---

## ЧАСТЬ 11: ГРАФИЧЕСКАЯ БИБЛИОТЕКА C+

### 11.1 Типы для графики

```c
// Базовые графические типы
typedef struct {
    int x, y;
} point;

typedef struct {
    int x1, y1, x2, y2;
} rect;

typedef struct {
    unsigned char r, g, b;
} rgb_color;

// Константы цветов
#define COLOR_BLACK   #000000
#define COLOR_WHITE   #FFFFFF
#define COLOR_RED     #FF0000
#define COLOR_GREEN   #00FF00
#define COLOR_BLUE    #0000FF
#define COLOR_YELLOW  #FFFF00

// Режимы рисования
enum draw_mode {
    MODE_SET,      // просто установить
    MODE_XOR,      // инвертировать (для выделения)
    MODE_CLEAR,    // очистить
    MODE_AND,      // AND с существующим
    MODE_OR        // OR с существующим
};
```

### 11.2 Основные графические функции

```c
// ============================================================
// УПРАВЛЕНИЕ ЭКРАНОМ
// ============================================================

/**
 * Очистить экран
 * @param fb - frame buffer
 */
void clear(array fb) {
    fill(fb, 0, 0, 639, 479, 0);
}

/**
 * Вывести буфер на физический экран
 * @param fb - frame buffer
 */
void display(array fb) {
    syscall(SYS_DISPLAY, fb);
}

/**
 * Установить видеорежим
 * @param mode - режим (0=текст, 1=графика)
 */
void set_video_mode(int mode) {
    video::mode = mode;
}

// ============================================================
// РИСОВАНИЕ ПРИМИТИВОВ
// ============================================================

/**
 * Нарисовать точку
 * @param fb - frame buffer
 * @param x, y - координаты
 * @param color - цвет (0 или 1)
 */
void draw_pixel(array fb, int x, int y, int color) {
    if (x >= 0 && x < 640 && y >= 0 && y < 480) {
        fb[x,y] = color;
    }
}

/**
 * Нарисовать линию (алгоритм Брезенхема)
 * @param fb - frame buffer
 * @param x1,y1 - начало
 * @param x2,y2 - конец
 * @param color - цвет
 */
void draw_line(array fb, int x1, int y1, int x2, int y2, int color) {
    int dx = ABS(x2 - x1);
    int dy = ABS(y2 - y1);
    int sx = (x1 < x2) ? 1 : -1;
    int sy = (y1 < y2) ? 1 : -1;
    int err = dx - dy;
    
    while (1) {
        fb[x1,y1] = color;
        if (x1 == x2 && y1 == y2) break;
        
        int e2 = 2 * err;
        if (e2 > -dy) {
            err -= dy;
            x1 += sx;
        }
        if (e2 < dx) {
            err += dx;
            y1 += sy;
        }
    }
}

/**
 * Заливка прямоугольника
 * @param fb - frame buffer
 * @param x1,y1 - левый верхний
 * @param x2,y2 - правый нижний
 * @param color - цвет
 */
void fill_rect(array fb, int x1, int y1, int x2, int y2, int color) {
    int x, y;
    for (y = y1; y <= y2; y++) {
        for (x = x1; x <= x2; x++) {
            fb[x,y] = color;
        }
    }
}

/**
 * Нарисовать прямоугольник (только контур)
 */
void draw_rect(array fb, int x1, int y1, int x2, int y2, int color) {
    draw_line(fb, x1, y1, x2, y1, color);  // верх
    draw_line(fb, x2, y1, x2, y2, color);  // право
    draw_line(fb, x1, y2, x2, y2, color);  // низ
    draw_line(fb, x1, y1, x1, y2, color);  // лево
}

/**
 * Нарисовать окружность (алгоритм mid-point)
 */
void draw_circle(array fb, int cx, int cy, int r, int color) {
    int x = 0;
    int y = r;
    int d = 1 - r;
    
    while (x <= y) {
        fb[cx+x, cy+y] = color;
        fb[cx+y, cy+x] = color;
        fb[cx-y, cy+x] = color;
        fb[cx-x, cy+y] = color;
        fb[cx-x, cy-y] = color;
        fb[cx-y, cy-x] = color;
        fb[cx+y, cy-x] = color;
        fb[cx+x, cy-y] = color;
        
        if (d < 0) {
            d += 2*x + 3;
        } else {
            d += 2*(x - y) + 5;
            y--;
        }
        x++;
    }
}

// ============================================================
// РАБОТА С ИЗОБРАЖЕНИЯМИ
// ============================================================

/**
 * Блочный перенос битов (BitBLT)
 * @param src - исходный буфер
 * @param dst - целевой буфер
 * @param sx,sy - исходные координаты
 * @param dx,dy - целевые координаты
 * @param w,h - ширина и высота
 * @param op - операция (MODE_SET, MODE_XOR и т.д.)
 */
void bitblt(array src, array dst, 
            int sx, int sy, int dx, int dy, 
            int w, int h, enum draw_mode op) {
    int x, y;
    int src_val, dst_val;
    
    for (y = 0; y < h; y++) {
        for (x = 0; x < w; x++) {
            src_val = src[sx+x, sy+y];
            dst_val = dst[dx+x, dy+y];
            
            switch (op) {
                case MODE_SET:
                    dst[dx+x, dy+y] = src_val;
                    break;
                case MODE_XOR:
                    dst[dx+x, dy+y] = src_val ^ dst_val;
                    break;
                case MODE_AND:
                    dst[dx+x, dy+y] = src_val & dst_val;
                    break;
                case MODE_OR:
                    dst[dx+x, dy+y] = src_val | dst_val;
                    break;
                case MODE_CLEAR:
                    dst[dx+x, dy+y] = 0;
                    break;
            }
        }
    }
}

/**
 * Загрузить иконку из данных
 */
void load_icon(array fb, int x, int y, word icon[16x16]) {
    bitblt(icon, fb, 0, 0, x, y, 16, 16, MODE_SET);
}

// ============================================================
// ТЕКСТ И ШРИФТЫ
// ============================================================

// Встроенный шрифт 8x8
array system_font[128x8];  // 128 символов по 8 пикселей высотой

/**
 * Вывести символ
 */
void put_char(array fb, int x, int y, char c, int color) {
    int row, col;
    array* glyph = &system_font[c * 8];  // каждый символ 8 строк
    
    for (row = 0; row < 8; row++) {
        word line = glyph[row];  // 8 бит - ширина символа
        for (col = 0; col < 8; col++) {
            if (line & (1 << (7-col))) {
                fb[x+col, y+row] = color;
            }
        }
    }
}

/**
 * Вывести строку
 */
void put_string(array fb, int x, int y, char* str, int color) {
    while (*str) {
        put_char(fb, x, y, *str++, color);
        x += 8;  // переходим к следующему символу
    }
}
```

### 11.3 Работа с мышью

```c
// ============================================================
// УПРАВЛЕНИЕ МЫШЬЮ
// ============================================================

// Состояние мыши
struct mouse_state {
    int x, y;           // позиция
    int left;           // левая кнопка (0/1)
    int middle;         // средняя кнопка
    int right;          // правая кнопка
};

// Текущее состояние мыши
struct mouse_state mouse;

/**
 * Инициализация мыши
 */
void mouse_init() {
    mouse.x = 320;
    mouse.y = 240;
    mouse.left = 0;
    mouse.middle = 0;
    mouse.right = 0;
    
    // Включить аппаратный курсор
    video::mouse_enable = 1;
}

/**
 * Получить текущее состояние мыши
 */
void mouse_update() {
    syscall(SYS_GET_MOUSE, &mouse);
}

/**
 * Установить позицию мыши
 */
void mouse_set_pos(int x, int y) {
    video::mouse_x = x;
    video::mouse_y = y;
    mouse.x = x;
    mouse.y = y;
}

/**
 * Установить форму курсора
 * @param cursor - массив 16x16 с формой курсора
 */
void mouse_set_cursor(array cursor[16x16]) {
    bitblt(cursor, video::mouse_ram, 0,0,0,0,16,16,MODE_SET);
}

// Предопределённые курсоры
array arrow_cursor[16x16] = {
    0b1000000000000000,
    0b1100000000000000,
    0b1110000000000000,
    0b1111000000000000,
    0b1111100000000000,
    0b1111110000000000,
    0b1111111000000000,
    0b1111111100000000,
    0b1111111110000000,
    0b1111111111000000,
    0b1111110000000000,
    0b1100110000000000,
    0b1000011000000000,
    0b0000001100000000,
    0b0000000110000000,
    0b0000000011000000
};

// ============================================================
// ОБРАБОТКА СОБЫТИЙ
// ============================================================

// Типы событий
enum event_type {
    EVENT_NONE,
    EVENT_MOUSE_DOWN,
    EVENT_MOUSE_UP,
    EVENT_MOUSE_MOVE,
    EVENT_KEY_DOWN,
    EVENT_KEY_UP,
    EVENT_TIMER
};

// Структура события
struct event {
    enum event_type type;
    int x, y;           // для мыши
    int key;            // для клавиатуры
    int button;         // для кнопок мыши
};

// Очередь событий
struct event event_queue[32];
int event_head = 0, event_tail = 0;

/**
 * Добавить событие в очередь
 */
void post_event(struct event* ev) {
    int next = (event_head + 1) % 32;
    if (next != event_tail) {
        event_queue[event_head] = *ev;
        event_head = next;
    }
}

/**
 * Получить следующее событие
 * @return 1 если событие есть, 0 если нет
 */
int get_next_event(struct event* ev) {
    if (event_head == event_tail) {
        return 0;
    }
    *ev = event_queue[event_tail];
    event_tail = (event_tail + 1) % 32;
    return 1;
}

/**
 * Главный цикл обработки событий
 */
void event_loop() {
    struct event ev;
    
    while (1) {
        while (get_next_event(&ev)) {
            switch (ev.type) {
                case EVENT_MOUSE_DOWN:
                    on_mouse_down(ev.x, ev.y, ev.button);
                    break;
                case EVENT_MOUSE_UP:
                    on_mouse_up(ev.x, ev.y, ev.button);
                    break;
                case EVENT_MOUSE_MOVE:
                    on_mouse_move(ev.x, ev.y);
                    break;
                case EVENT_KEY_DOWN:
                    on_key_down(ev.key);
                    break;
                default:
                    break;
            }
        }
        wait(1);
    }
}

// Обработчики (пользователь определяет)
void on_mouse_down(int x, int y, int button) { }
void on_mouse_up(int x, int y, int button) { }
void on_mouse_move(int x, int y) { }
void on_key_down(int key) { }
```

---

## ЧАСТЬ 12: СИСТЕМНЫЕ ВЫЗОВЫ И РАБОТА С ЖЕЛЕЗОМ

### 12.1 Системные вызовы

```c
// Номера системных вызовов
#define SYS_DISPLAY   1   // обновить экран
#define SYS_GET_MOUSE 2   // прочитать мышь
#define SYS_GET_KEY   3   // прочитать клавиатуру
#define SYS_WAIT      4   // задержка
#define SYS_BEEP      5   // звуковой сигнал
#define SYS_READ_DISK 6   // чтение с диска
#define SYS_WRITE_DISK 7  // запись на диск

/**
 * Общий системный вызов
 */
int syscall(int number, ...) {
    asm {
        "trap $0"
    }
}

/**
 * Задержка в миллисекундах
 */
void wait(int ms) {
    syscall(SYS_WAIT, ms);
}

/**
 * Звуковой сигнал
 */
void beep() {
    syscall(SYS_BEEP);
}
```

### 12.2 Прямой доступ к регистрам

```c
// Адреса регистров видеоконтроллера
#define VIDEO_BASE   0170000b
#define VIDEO_MODE   (*(word*)0170010b)
#define VIDEO_MOUSE_X (*(word*)0170012b)
#define VIDEO_MOUSE_Y (*(word*)0170014b)
#define VIDEO_MOUSE_EN (*(word*)0170016b)

// Работа с регистрами через синтаксис C+
word* video = @display;
video[1000] = 0xFFFF;

// Установка режима через регистры
void set_display_mode(int mode) {
    VIDEO_MODE = mode;
}

// Включение/выключение курсора
void show_cursor(int show) {
    VIDEO_MOUSE_EN = show ? 1 : 0;
}
```

### 12.3 Работа с памятью

```c
// Прямая запись в память
void poke(word addr, word value) {
    *(word*)addr = value;
}

// Прямое чтение из памяти
word peek(word addr) {
    return *(word*)


# Eng(English version)


# COMPLETE C+ LANGUAGE REFERENCE
## Version 1.0 (1974)

---

## PART 1: GENERAL INFORMATION

### 1.1 Language Philosophy

C+ was created as a graphical extension of the C language. The main principles are:

| Principle | Description |
|:--------|:---------|
| **Direct access to the hardware** | Minimal abstraction between code and graphical hardware |
| **Simplified graphics** | Syntax that is intuitive for working with pixels and the screen |
| **Experimental types** | New data types for working with graphical objects |
| **B legacy** | Preserving the simplicity and efficiency of the B/early C language |

### 1.2 Target platform

| Feature | Value |
|:---------------|:---------|
| **Processor** | 16-bit microprogrammable CPU |
| **Memory** | 128-512 KB |
| **Display** | 606 x 808 pixels (portrait mode), monochrome |
| **Input devices** | Keyboard + three-button mouse |
| **Network** | Ethernet |

---

## PART 2: LEXIS AND SYNTAX

### 2.1 Character set

```
Letters:        A-Z a-z _
Numbers:        0-9
Special characters:  + - * / = ! < > & | ^ ^ % . , ; : ? ' " ( ) [ ] { } #
Whitespace:   space, tab, newline
```

### 2.2 Keywords

```
auto        array       bit        break       case        char
clear       color       continue    default     display     do
draw        else        fill        for         goto        if
int         line        mouse       pixel       register    return
short       sizeof      struct      switch      typedef     unsigned
void        wait        while       word
```

### 2.3 Comments

```c
// Single-line comment

/* Multiline
   comment */
    return *(word*)
