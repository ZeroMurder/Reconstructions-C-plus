Язык который можно и нужно улучшать под себя и тд , джанный язык не мой это реконстркция из непроверенных источников якобы они создали Xerox PARC но это не точно сам язык мертв а данных особо не было о нем но это так чисто есть значит есть нету значит вот появился.
Если язык был то к нему отношение не имею только реконстрктивное отношение, если не было то тогда полная моя работа по воссоздании из разных источников полная Mit lisense типо берете делаете че хотите мне пофиг это наоборот хороший пример работы с жжелезом прям нормально.
A language that can and should be improved to suit your needs, etc. The C+ language is not mine; it is a reconstruction based on unverified sources, claiming that they created Xerox PARC. However, it is uncertain whether the language itself is dead, and there is limited information about it. Nevertheless, it is a fact that the language exists.
If the language existed, I have no involvement with it other than the reconstruction. If it did not exist, then my full effort was to recreate it from various sources. This is a good example of working with hardware.

# COMPLETE C+ LANGUAGE REFERENCE
## Version 1.0 (1974)

---

## PART 1: GENERAL INFORMATION

### 1.1 Language Philosophy

C+ was created as a graphical extension of the C language. Core principles:

| Principle | Description |
|:----------|:------------|
| **Direct hardware access** | Minimum abstractions between code and graphics hardware |
| **Graphics simplification** | Intuitive syntax for working with pixels and screen |
| **Experimental types** | New data types for working with graphical objects |
| **B legacy** | Maintaining the simplicity and efficiency of B/early C |

### 1.2 Target Platform

| Characteristic | Value |
|:---------------|:------|
| **Processor** | 16-bit microprogrammable CPU |
| **Memory** | 128-512 KB |
| **Display** | 606 x 808 pixels (portrait mode), monochrome |
| **Input devices** | Keyboard + three-button mouse |
| **Network** | Ethernet |

---

## PART 2: LEXICAL ELEMENTS AND SYNTAX

### 2.1 Character Set

```
Letters:      A-Z a-z _
Digits:       0-9
Special:      + - * / = ! < > & | ^ ^ % . , ; : ? ' " ( ) [ ] { } #
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

/* Multi-line
   comment */
```

### 2.4 Identifiers

- Length: up to 31 characters (first 8 significant for linker)
- Case-sensitive
- Begin with letter or underscore

---

## PART 3: DATA TYPES

### 3.1 Basic Types

| Type | Size | Range | Description |
|:-----|:-----|:------|:------------|
| `char` | 8 bits | -128..127 or 0..255 | Character or small integer |
| `short` | 16 bits | -32768..32767 | Short integer |
| `int` | 16 bits | -32768..32767 | Integer |
| `unsigned` | 16 bits | 0..65535 | Unsigned integer |
| `long` | 32 bits | -2^31..2^31-1 | Long integer |
| `float` | 32 bits | ~1e-38..1e38 | Floating point |
| `double` | 64 bits | ~1e-308..1e308 | Double precision |
| `void` | 0 | - | Empty type |

### 3.2 C+ Special Types

| Type | Size | Description | Example |
|:-----|:-----|:------------|:--------|
| `pixel` | 1 bit | Pixel value | `pixel p = 1;` |
| `color` | 24 bits | Experimental color | `color red = #FF0000;` |
| `point` | 32 bits | Coordinates (x,y) | `point p = {100,200};` |
| `rect` | 64 bits | Rectangle (x1,y1,x2,y2) | `rect r = {0,0,100,100};` |
| `mouse` | 32 bits | Mouse position + buttons | `mouse m;` |
| `bitmap` | Variable | Bit array | `bitmap icon[32x32];` |
| `word` | 16 bits | Machine word | `word* video = 0170000b;` |

### 3.3 Derived Types

| Type | Syntax | Example |
|:-----|:-------|:--------|
| Pointer | `type*` | `int* ptr;` |
| Array | `type[N]` | `int buf[100];` |
| Structure | `struct { ... }` | `struct point { int x; int y; };` |
| Union | `union { ... }` | `union { int i; char c; };` |
| Enumeration | `enum { ... }` | `enum bool { FALSE, TRUE };` |

### 3.4 Special Array Syntax

```c
// Regular C
int screen[606][808];
screen[100][200] = 1;

// C+ — simplified syntax
array screen[606x808];          // 2D array with single declaration
screen[100,200] = 1;            // Intuitive coordinate access

// Other variations
array fb[640x480];                // Frame buffer
array icon[16x16];                // Icon
array font[128x8];                 // Font
```

---

## PART 4: VARIABLES AND DECLARATIONS

### 4.1 Storage Classes

| Class | Description |
|:------|:------------|
| `auto` | Local variable (default) |
| `register` | Request to store in register |
| `static` | Static variable (retains value) |
| `extern` | External variable (in another file) |

```c
auto int x = 10;           // Local variable
register int counter;      // In register (for speed)
static int global_count;   // Static variable
extern array screen[];     // Defined elsewhere
```

### 4.2 Initialization

```c
int i = 100;
char c = 'A';
point origin = {0, 0};
rect screen_rect = {0, 0, 605, 807};
color white = #FFFFFF;

array fb[640x480] = {0};     // Whole array set to zero
```

### 4.3 Constants

```c
// Integer
int i = 1234;       // Decimal
int o = 0123;       // Octal (starts with 0)
int h = 0x1A3F;     // Hexadecimal

// Floating point
float f = 3.14159;
double d = 2.7e-10;

// Character
char nl = '\n';     // Newline character
char tab = '\t';    // Tab character
char c = 'A';       // Regular character

// String
char* msg = "Hello!";
```

### 4.4 Automatic Type Inference

```c
auto x = 100;           // Type int
auto y = 3.14;          // Type float
auto p = &x;            // Type int*
auto name = "C+";       // Type char*
```

---

## PART 5: OPERATORS

### 5.1 Arithmetic Operators

| Operator | Meaning | Example |
|:---------|:--------|:--------|
| `+` | Addition | `a + b` |
| `-` | Subtraction | `a - b` |
| `*` | Multiplication | `a * b` |
| `/` | Division | `a / b` |
| `%` | Modulo | `a % b` |
| `++` | Increment | `i++` or `++i` |
| `--` | Decrement | `i--` or `--i` |

### 5.2 Comparison Operators

| Operator | Meaning | Example |
|:---------|:--------|:--------|
| `==` | Equal to | `a == b` |
| `!=` | Not equal to | `a != b` |
| `<` | Less than | `a < b` |
| `>` | Greater than | `a > b` |
| `<=` | Less than or equal | `a <= b` |
| `>=` | Greater than or equal | `a >= b` |

### 5.3 Logical Operators

| Operator | Meaning | Example |
|:---------|:--------|:--------|
| `&&` | Logical AND | `a && b` |
| `\|\|` | Logical OR | `a \|\| b` |
| `!` | Logical NOT | `!a` |

### 5.4 Bitwise Operators

| Operator | Meaning | Example |
|:---------|:--------|:--------|
| `&` | Bitwise AND | `a & b` |
| `\|` | Bitwise OR | `a \| b` |
| `^` | Bitwise XOR | `a ^ b` |
| `~` | Bitwise NOT | `~a` |
| `<<` | Left shift | `a << 2` |
| `>>` | Right shift | `a >> 2` |

### 5.5 Assignment Operators

| Operator | Equivalent | Example |
|:---------|:-----------|:--------|
| `=` | Simple assignment | `a = b` |
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

### 5.6 C+ Special Operators

| Operator | Meaning | Example |
|:---------|:--------|:--------|
| `[x,y]` | 2D array access | `screen[100,200]` |
| `@` | Take video memory address | `@display` |
| `#` | Color constant | `#FF0000` |
| `::` | System register access | `video::mode` |

---

## PART 6: CONTROL STRUCTURES

### 6.1 Conditional `if`

```c
if (condition) {
    // code
}

if (condition) {
    // code
} else {
    // other code
}

if (x < 0) {
    x = 0;
} else if (x > max_x) {
    x = max_x;
} else {
    // normal case
}
```

### 6.2 Selection `switch`

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

### 6.3 `while` Loop

```c
while (condition) {
    // loop body
}

// Infinite loop
while (1) {
    handle_events();
}
```

### 6.4 `do-while` Loop

```c
do {
    // executes at least once
} while (condition);
```

### 6.5 `for` Loop

```c
for (init; condition; increment) {
    // body
}

// Example
for (i = 0; i < 640; i++) {
    screen[i,240] = 1;  // horizontal line
}
```

### 6.6 Jump Statements

| Statement | Purpose |
|:----------|:--------|
| `break;` | Exit loop or switch |
| `continue;` | Skip to next iteration |
| `goto label;` | Unconditional jump |
| `return;` | Return from function |
| `return value;` | Return with value |

---

## PART 7: FUNCTIONS

### 7.1 Function Declarations

```c
// Return type  name(parameters)
int add(int a, int b) {
    return a + b;
}

// No return value
void clear_screen() {
    fill(screen, 0, 0, 605, 807, 0);
}

// With default parameters (experimental!)
void draw_point(int x, int y, int color = 1) {
    screen[x,y] = color;
}
```

### 7.2 Old Style (from B/early C)

```c
draw(x, y, color)
int x, y, color;  // parameters declared separately
{
    screen[x,y] = color;
}
```

### 7.3 Variable Argument Functions

```c
printf(format, ...)
char* format;
{
    // process variable arguments
}
```

---

## PART 8: STRUCTURES AND UNIONS

### 8.1 Structure Definitions

```c
// Simple structure
struct point {
    int x;
    int y;
};

// Nested structure
struct rectangle {
    struct point p1;
    struct point p2;
};

// Structure with bit fields
struct video_register {
    unsigned mode : 2;
    unsigned enable : 1;
    unsigned int : 5;  // skip 5 bits
    unsigned page : 8;
};
```

### 8.2 Using Structures

```c
// Declaration
struct point p;
struct rectangle r;

// Initialization
struct point origin = {0, 0};
struct point cursor = {320, 240};

// Field access
p.x = 100;
p.y = 200;
x = p.x;

// Structure assignment
p = origin;

// Pointers to structures
struct point* ptr = &origin;
(*ptr).x = 50;
ptr->y = 60;  // -> operator
```

### 8.3 Unions

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

## PART 9: POINTERS AND ADDRESSING

### 9.1 Pointer Basics

```c
int x = 10;
int* ptr = &x;     // ptr points to x
int y = *ptr;      // y = 10

*ptr = 20;         // x is now 20
```

### 9.2 Pointer Arithmetic

```c
int arr[10];
int* p = arr;      // points to arr[0]
p++;               // now points to arr[1]
int* q = arr + 5;  // points to arr[5]
```

### 9.3 Pointers to Video Memory

```c
// Direct video memory access
word* video_mem = (word*)0170000b;

// Working with memory as array
video_mem[1000] = 0xFFFF;  // light up 16 pixels

// Via C+ special syntax
word* fb = @display;        // get display address
```

### 9.4 Function Pointers

```c
// Function pointer type definition
void (*handler)(int, int);

// Assignment
handler = draw_point;

// Call
handler(100, 200);
```

---

## PART 10: PREPROCESSOR

### 10.1 Preprocessor Directives

| Directive | Purpose | Example |
|:----------|:--------|:--------|
| `#define` | Macro definition | `#define WIDTH 640` |
| `#undef` | Undefine macro | `#undef WIDTH` |
| `#include` | Insert file | `#include "graphics.h"` |
| `#ifdef` | If defined | `#ifdef DEBUG` |
| `#ifndef` | If not defined | `#ifndef HEADER_H` |
| `#if` | Conditional compilation | `#if WIDTH > 600` |
| `#else` | Else | `#else` |
| `#elif` | Else if | `#elif WIDTH == 640` |
| `#endif` | End condition | `#endif` |
| `#line` | Change line number | `#line 100 "file.c"` |
| `#error` | Error message | `#error "Version mismatch"` |
| `#pragma` | Compiler instruction | `#pragma optimize` |

### 10.2 Macro Examples

```c
// Constants
#define SCREEN_WIDTH  606
#define SCREEN_HEIGHT 808
#define WHITE 1
#define BLACK 0

// Parameterized macros
#define MIN(a,b) ((a) < (b) ? (a) : (b))
#define MAX(a,b) ((a) > (b) ? (a) : (b))
#define ABS(x) ((x) < 0 ? -(x) : (x))

// Graphics macros
#define SETPIXEL(arr,x,y,val) (arr[x,y] = (val))
#define GETPIXEL(arr,x,y) (arr[x,y])
```

### 10.3 Predefined Macros

| Macro | Meaning |
|:------|:--------|
| `__LINE__` | Current line |
| `__FILE__` | Current file |
| `__DATE__` | Compilation date |
| `__TIME__` | Compilation time |
| `__C_PLUS__` | Always defined for C+ |

---

## PART 11: C+ GRAPHICS LIBRARY

### 11.1 Graphics Types

```c
// Basic graphics types
typedef struct {
    int x, y;
} point;

typedef struct {
    int x1, y1, x2, y2;
} rect;

typedef struct {
    unsigned char r, g, b;
} rgb_color;

// Color constants
#define COLOR_BLACK   #000000
#define COLOR_WHITE   #FFFFFF
#define COLOR_RED     #FF0000
#define COLOR_GREEN   #00FF00
#define COLOR_BLUE    #0000FF
#define COLOR_YELLOW  #FFFF00

// Drawing modes
enum draw_mode {
    MODE_SET,      // simple set
    MODE_XOR,      // invert (for highlighting)
    MODE_CLEAR,    // clear
    MODE_AND,      // AND with existing
    MODE_OR        // OR with existing
};
```

### 11.2 Basic Graphics Functions

```c
// ============================================================
// SCREEN MANAGEMENT
// ============================================================

/**
 * Clear the screen
 * @param fb - frame buffer
 */
void clear(array fb) {
    fill(fb, 0, 0, 639, 479, 0);
}

/**
 * Display buffer to physical screen
 * @param fb - frame buffer
 */
void display(array fb) {
    syscall(SYS_DISPLAY, fb);
}

/**
 * Set video mode
 * @param mode - mode (0=text, 1=graphics)
 */
void set_video_mode(int mode) {
    video::mode = mode;
}

// ============================================================
// PRIMITIVE DRAWING
// ============================================================

/**
 * Draw a pixel
 * @param fb - frame buffer
 * @param x, y - coordinates
 * @param color - color (0 or 1)
 */
void draw_pixel(array fb, int x, int y, int color) {
    if (x >= 0 && x < 640 && y >= 0 && y < 480) {
        fb[x,y] = color;
    }
}

/**
 * Draw a line (Bresenham's algorithm)
 * @param fb - frame buffer
 * @param x1,y1 - start
 * @param x2,y2 - end
 * @param color - color
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
 * Fill rectangle
 * @param fb - frame buffer
 * @param x1,y1 - top-left
 * @param x2,y2 - bottom-right
 * @param color - color
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
 * Draw rectangle (outline only)
 */
void draw_rect(array fb, int x1, int y1, int x2, int y2, int color) {
    draw_line(fb, x1, y1, x2, y1, color);  // top
    draw_line(fb, x2, y1, x2, y2, color);  // right
    draw_line(fb, x1, y2, x2, y2, color);  // bottom
    draw_line(fb, x1, y1, x1, y2, color);  // left
}

/**
 * Draw circle (mid-point algorithm)
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
// IMAGE OPERATIONS
// ============================================================

/**
 * Bit block transfer (BitBLT)
 * @param src - source buffer
 * @param dst - destination buffer
 * @param sx,sy - source coordinates
 * @param dx,dy - destination coordinates
 * @param w,h - width and height
 * @param op - operation (MODE_SET, MODE_XOR, etc.)
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
 * Load icon from data
 */
void load_icon(array fb, int x, int y, word icon[16x16]) {
    bitblt(icon, fb, 0, 0, x, y, 16, 16, MODE_SET);
}

// ============================================================
// TEXT AND FONTS
// ============================================================

// Built-in 8x8 font
array system_font[128x8];  // 128 characters, 8 pixels high each

/**
 * Output a character
 */
void put_char(array fb, int x, int y, char c, int color) {
    int row, col;
    array* glyph = &system_font[c * 8];  // each character is 8 rows
    
    for (row = 0; row < 8; row++) {
        word line = glyph[row];  // 8 bits - character width
        for (col = 0; col < 8; col++) {
            if (line & (1 << (7-col))) {
                fb[x+col, y+row] = color;
            }
        }
    }
}

/**
 * Output a string
 */
void put_string(array fb, int x, int y, char* str, int color) {
    while (*str) {
        put_char(fb, x, y, *str++, color);
        x += 8;  // move to next character
    }
}
```

### 11.3 Mouse Operations

```c
// ============================================================
// MOUSE CONTROL
// ============================================================

// Mouse state
struct mouse_state {
    int x, y;           // position
    int left;           // left button (0/1)
    int middle;         // middle button
    int right;          // right button
};

// Current mouse state
struct mouse_state mouse;

/**
 * Initialize mouse
 */
void mouse_init() {
    mouse.x = 320;
    mouse.y = 240;
    mouse.left = 0;
    mouse.middle = 0;
    mouse.right = 0;
    
    // Enable hardware cursor
    video::mouse_enable = 1;
}

/**
 * Get current mouse state
 */
void mouse_update() {
    syscall(SYS_GET_MOUSE, &mouse);
}

/**
 * Set mouse position
 */
void mouse_set_pos(int x, int y) {
    video::mouse_x = x;
    video::mouse_y = y;
    mouse.x = x;
    mouse.y = y;
}

/**
 * Set cursor shape
 * @param cursor - 16x16 cursor shape array
 */
void mouse_set_cursor(array cursor[16x16]) {
    bitblt(cursor, video::mouse_ram, 0,0,0,0,16,16,MODE_SET);
}

// Predefined cursors
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
// EVENT HANDLING
// ============================================================

// Event types
enum event_type {
    EVENT_NONE,
    EVENT_MOUSE_DOWN,
    EVENT_MOUSE_UP,
    EVENT_MOUSE_MOVE,
    EVENT_KEY_DOWN,
    EVENT_KEY_UP,
    EVENT_TIMER
};

// Event structure
struct event {
    enum event_type type;
    int x, y;           // for mouse
    int key;            // for keyboard
    int button;         // for mouse buttons
};

// Event queue
struct event event_queue[32];
int event_head = 0, event_tail = 0;

/**
 * Add event to queue
 */
void post_event(struct event* ev) {
    int next = (event_head + 1) % 32;
    if (next != event_tail) {
        event_queue[event_head] = *ev;
        event_head = next;
    }
}

/**
 * Get next event
 * @return 1 if event exists, 0 if not
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
 * Main event loop
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

// Handlers (user defines)
void on_mouse_down(int x, int y, int button) { }
void on_mouse_up(int x, int y, int button) { }
void on_mouse_move(int x, int y) { }
void on_key_down(int key) { }
```

---

## PART 12: SYSTEM CALLS AND HARDWARE ACCESS

### 12.1 System Calls

```c
// System call numbers
#define SYS_DISPLAY   1   // update screen
#define SYS_GET_MOUSE 2   // read mouse
#define SYS_GET_KEY   3   // read keyboard
#define SYS_WAIT      4   // delay
#define SYS_BEEP      5   // sound beep
#define SYS_READ_DISK 6   // read from disk
#define SYS_WRITE_DISK 7  // write to disk

/**
 * General system call
 */
int syscall(int number, ...) {
    asm {
        "trap $0"
    }
}

/**
 * Delay in milliseconds
 */
void wait(int ms) {
    syscall(SYS_WAIT, ms);
}

/**
 * Sound beep
 */
void beep() {
    syscall(SYS_BEEP);
}
```

### 12.2 Direct Register Access

```c
// Video controller register addresses
#define VIDEO_BASE   0170000b
#define VIDEO_MODE   (*(word*)0170010b)
#define VIDEO_MOUSE_X (*(word*)0170012b)
#define VIDEO_MOUSE_Y (*(word*)0170014b)
#define VIDEO_MOUSE_EN (*(word*)0170016b)

// Register access via C+ syntax
word* video = @display;
video[1000] = 0xFFFF;

// Set mode via registers
void set_display_mode(int mode) {
    VIDEO_MODE = mode;
}

// Enable/disable cursor
void show_cursor(int show) {
    VIDEO_MOUSE_EN = show ? 1 : 0;
}
```

### 12.3 Memory Operations

```c
// Direct memory write
void poke(word addr, word value) {
    *(word*)addr = value;
}

// Direct memory read
word peek(word addr) {
    return *(word*)addr;
}
```

---

## PART 13: PROGRAM EXAMPLES

### 13.1 "Hello, World!" Graphical

```c
// hello.c - graphical version of Hello World

#include "graphics.h"

array screen[640x480];

main() {
    clear(screen);
    put_string(screen, 200, 240, "Hello!", COLOR_WHITE);
    display(screen);
    
    while (1) ;
}
```

### 13.2 Mouse Drawing

```c
// paint.c - simple paint program

#include "graphics.h"

array canvas[640x480];
int drawing = 0;
int last_x, last_y;

void on_mouse_down(int x, int y, int button) {
    drawing = 1;
    last_x = x;
    last_y = y;
    canvas[x,y] = 1;
    display(canvas);
}

void on_mouse_up(int x, int y, int button) {
    drawing = 0;
}

void on_mouse_move(int x, int y) {
    if (drawing) {
        draw_line(canvas, last_x, last_y, x, y, 1);
        last_x = x;
        last_y = y;
        display(canvas);
    }
}

main() {
    clear(canvas);
    display(canvas);
    
    event_loop();
}
```

### 13.3 Animation

```c
// bounce.c - bouncing ball animation

#include "graphics.h"

array fb[640x480];

struct ball {
    int x, y;
    int dx, dy;
    int r;
};

struct ball b = {320, 240, 2, 1, 10};

void update_ball() {
    draw_circle(fb, b.x, b.y, b.r, MODE_XOR);
    
    b.x += b.dx;
    b.y += b.dy;
    
    if (b.x < b.r || b.x > 640 - b.r) {
        b.dx = -b.dx;
        beep();
    }
    if (b.y < b.r || b.y > 480 - b.r) {
        b.dy = -b.dy;
        beep();
    }
    
    draw_circle(fb, b.x, b.y, b.r, MODE_SET);
}

main() {
    clear(fb);
    
    while (1) {
        update_ball();
        display(fb);
        wait(20);
    }
}
```

---

## PART 14: C+ DIFFERENCES FROM C

| Feature | C | C+ |
|:--------|:--|:---|
| Arrays | `int a[10][20];` | `array a[10x20];` |
| Access | `a[i][j]` | `a[i,j]` |
| Graphics | No | Built-in |
| `color` type | No | Yes |
| Mouse support | No | Built-in |
| BitBLT | No | Yes |
| Direct video access | Via pointers | `@` special syntax |

---

## PART 15: SUMMARY

C+ (1974) — an experimental extension of the C language for graphical programming, offering:

- Simplified syntax for 2D arrays
- Built-in graphics primitives
- Mouse support at language level
- Direct video memory access
- Experimental data types
