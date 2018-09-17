



C与Go的区别





# [Hyperpolyglot](http://hyperpolyglot.org/)

C, Go

*a side-by-side reference sheet*

[grammar and invocation](http://hyperpolyglot.org/c#grammar-invocation) | [variables and expressions](http://hyperpolyglot.org/c#variables-expressions) | [arithmetic and logic](http://hyperpolyglot.org/c#arithmetic-logic) | [strings](http://hyperpolyglot.org/c#strings) | [regexes](http://hyperpolyglot.org/c#regexes) | [dates and time](http://hyperpolyglot.org/c#dates-time) | [fixed-length-arrays](http://hyperpolyglot.org/c#fixed-length-arrays) | [resizable arrays](http://hyperpolyglot.org/c#resizable-arrays) | [dictionaries](http://hyperpolyglot.org/c#dictionaries) | [functions](http://hyperpolyglot.org/c#functions) | [execution control](http://hyperpolyglot.org/c#execution-control) | [concurrency](http://hyperpolyglot.org/c#concurrency) | [file handles](http://hyperpolyglot.org/c#file-handles) | [files](http://hyperpolyglot.org/c#files) | [file formats](http://hyperpolyglot.org/c#file-fmt)| [directories](http://hyperpolyglot.org/c#directories) | [processes and environment](http://hyperpolyglot.org/c#processes-environment) | [option parsing](http://hyperpolyglot.org/c#option-parsing) | [libraries and namespaces](http://hyperpolyglot.org/c#libraries-namespaces) | [objects](http://hyperpolyglot.org/c#objects) | [user-defined types](http://hyperpolyglot.org/c#user-defined-types) | [c preprocessor macros](http://hyperpolyglot.org/c#cpp-macros) | [net and web](http://hyperpolyglot.org/c#net-web) | [unit tests](http://hyperpolyglot.org/c#unit-tests) | [debugging and profiling](http://hyperpolyglot.org/c#debugging-profiling)

| [version](http://hyperpolyglot.org/c#version-note)           |                                                              |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              | [c](http://hyperpolyglot.org/c#c)                            | [go](http://hyperpolyglot.org/c#go)                          |
| [version used](http://hyperpolyglot.org/c#version-used-note) | *C11*, *gcc 4.8*, *clang 3.5*                                | *1.10*                                                       |
| [show version](http://hyperpolyglot.org/c#show-version-note) | $ gcc --version                                              | $ go version                                                 |
| [implicit prologue](http://hyperpolyglot.org/c#implicit-prologue-note) | #include <errno.h> #include <stdlib.h> #include <stdio.h> #include <string.h> #include <time.h> #include <wchar.h> | import "fmt"                                                 |
| [grammar and invocation](http://hyperpolyglot.org/c#grammar-invocation-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [hello world](http://hyperpolyglot.org/c#hello-world-note)   | $ cat hello.c #include <stdio.h>  int main(int argc, char **argv) {   printf("Hello, World!\n"); }  $ gcc hello.c  $ ./a.out Hello, World! | $ cat hello.go package main import "fmt"  func main() {   fmt.Printf("Hello, World!\n") }  $ go build hello.go  $ ./hello Hello, World! |
| [file suffixes](http://hyperpolyglot.org/c#file-suffixes-note) *source, header, object file* | .c .h .o                                                     | .go *none* *none*                                            |
| [statement separator](http://hyperpolyglot.org/c#stmt-separator-note) | ;                                                            | ; *or sometimes newline*  *a new line terminates a statement when the last token on the line is  (1) an identifier,  (2) a numeric, character, or string literal,  (3) one of the keywords* break, continue,       fallthrough, *or* return,   *(4) one of* ++, --, ), ], *or* } |
| [block delimiters](http://hyperpolyglot.org/c#block-delimiters-note) | { *…* }                                                      | { *…* }                                                      |
| [end-of-line comment](http://hyperpolyglot.org/c#eol-comment-note) | // *comment*                                                 | // *comment*                                                 |
| [multiple line comment](http://hyperpolyglot.org/c#multiple-line-comment-note) | /* *comment line* *another line* */                          | /* *comment line* *another line* */                          |
| [variables and expressions](http://hyperpolyglot.org/c#variables-expressions-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [variable](http://hyperpolyglot.org/c#local-var-note)        | /* if inside function, memory allocated on stack: */ int i; int j = 3;  /* memory allocated on heap: */ int *ptr = malloc(sizeof *ptr); /* if malloc fails, it returns NULL and sets errno to ENOMEM */ *ptr = 7; | // memory allocated on stack: var i int  // allocated on stack; type inferred from literal: j := 3  // memory allocated on heap: ptr := new(int) *ptr = 7 |
| [free heap](http://hyperpolyglot.org/c#free-heap-note)       | free(ptr);                                                   | *none; uses garbage collection*                              |
| [global variable](http://hyperpolyglot.org/c#global-var-note) | /* in foo.c, outside of any function: */ int x = 7;  /* to declare in bar.c: */ extern int x; | // foo.go: package foo  // capitalized top-level identifiers are exported: var X = 7  // bar.go: package bar import foo  // package scope: var y = 3  func baz() {   // local scope:   var z = 5    fmt.Println(foo.X + y + z) } |
| [uninitialized variable](http://hyperpolyglot.org/c#uninitialized-var-note) | *The behavior of reading from uninitialized stack variables or unitialized memory allocated by* malloc *is undefined.Global and static variables are zero-initialized.Heap variables allocated by* calloc *have their bytes zeroed.* | *Every type has a zero value. For numeric types it is zero and for strings it is the empty string.* |
| [compile time constant](http://hyperpolyglot.org/c#compile-time-const-note) | /* usually preprocessor is used: */ #define PI 3.14          | const Pi = 3.14                                              |
| [immutable variable](http://hyperpolyglot.org/c#immutable-var-note) | const int i = rand();                                        | *none*                                                       |
| [assignment](http://hyperpolyglot.org/c#assignment-note)     | i = 3;                                                       | // defines variable of appropriate type: i := 3  // variable must already be declared: i = 3 |
| [parallel assignment](http://hyperpolyglot.org/c#parallel-assignment-note) | *none*                                                       | // define variables of appropriate type: m, n := 3, 7  // x and y must already be declared: x, y = 2, 8 |
| [swap](http://hyperpolyglot.org/c#swap-note)                 | int x = 1, y = 2, tmp;  tmp = x; x = y; y = tmp;             | x, y = y, x                                                  |
| [compound assignment](http://hyperpolyglot.org/c#compound-assignment-note) | *arithmetic:* += -= *= /= %=  *bit:* <<= >>= &= \|= ^=       | *arithmetic:* += -= *= /= %=  *bit:* <<= >>= &= \|= ^=       |
| [increment and decrement](http://hyperpolyglot.org/c#incr-decr-note) | *premodifiers:* ++i --i  *postmodifiers:* i++ i--            | *postmodifiers only; cannot be used in expressions:* i++ i-- |
| [address](http://hyperpolyglot.org/c#addr-note)              | int i = 3; int* ptr = &i;                                    | i := 3  var ptr *int ptr = &i ptr2 := &i                     |
| [dereference](http://hyperpolyglot.org/c#dereference-note)   | int i2 = *ptr;                                               | i2 := *ptr                                                   |
| [type size](http://hyperpolyglot.org/c#type-size-note)       | /* put type inside parens: */ sizeof (int)  /* expressions and values don't require parens: */ sizeof 1 + 1 | import "unsafe"  // use expression or name of variable with type: unsafe.Sizeof(i) unsafe.Sizeof(1 + 1) |
| [address arithmetic](http://hyperpolyglot.org/c#addr-arith-note) | int a[] = {3, 2, 1, 0};  for (int *p = a; *p; ++p) {   printf("%d\n", *p); } | *none*                                                       |
| [null](http://hyperpolyglot.org/c#null-note)                 | /* pointer types only: */ NULL                               | // cannot be stored in numeric or string variable: nil       |
| [null test](http://hyperpolyglot.org/c#null-test-note)       | ptr == NULL                                                  | ptr == nil                                                   |
| [conditional expression](http://hyperpolyglot.org/c#conditional-expr-note) | x > 0 ? x : -x                                               | *none*                                                       |
| [arithmetic and logic](http://hyperpolyglot.org/c#arithmetic-logic-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [boolean type](http://hyperpolyglot.org/c#boolean-type-note) | int  /* includes type for consistency with C++: */ #include <stdbool.h>  bool | bool                                                         |
| [true and false](http://hyperpolyglot.org/c#true-false-note) | 1 0  /* includes identifiers for consistency with C++: */ #include <stdbool.h>  true false | true false                                                   |
| [falsehoods](http://hyperpolyglot.org/c#falsehoods-note)     | 0 0.0 NULL false                                             | false                                                        |
| [logical operators](http://hyperpolyglot.org/c#logical-op-note) | && \|\| !                                                    | && \|\| !                                                    |
| [relational operators](http://hyperpolyglot.org/c#relational-op-note) | == != < > <= >=                                              | == != < > <= >=                                              |
| [integer type](http://hyperpolyglot.org/c#int-type-note)     | signed char *1+ bytes* short int *2+ bytes* int *2+ bytes* long int *4+ bytes* long long int *4+ bytes*  *types with portable sizes are defined in* stdint.h: int8_t int16_t int32_t int64_t | int int8 int16 int32 int64                                   |
| [unsigned type](http://hyperpolyglot.org/c#unsigned-type-note) | unsigned char: *1+ bytes* unsigned short int *2 bytes+* unsigned int *2 bytes+* unsigned long int *4+ bytes* unsigned long long int *4+ bytes*  *types with portable sizes are defined in* stdint.h: uint8_t uint16_t uint32_t uint64_t | uint8 (byte) uint16 uint32 uint64                            |
| [float type](http://hyperpolyglot.org/c#float-type-note)     | float *4 bytes* double *8 bytes* long double *16 bytes*  *registers may be larger on some systems* | float32 float64                                              |
| [arithmetic operators](http://hyperpolyglot.org/c#arith-op-note) | + - * / %                                                    | + - * / %                                                    |
| [integer division](http://hyperpolyglot.org/c#int-div-note)  | 3 / 7                                                        | 3 / 7                                                        |
| [integer division by zero](http://hyperpolyglot.org/c#int-div-zero-note) | *system dependent; process often sent a* SIGFPE *signal*     | *on Unix, process sent a* SIGFPE *signal*                    |
| [float division](http://hyperpolyglot.org/c#float-div-note)  | 3 / (float)7                                                 | 3 / float32(7)                                               |
| [float division by zero](http://hyperpolyglot.org/c#float-div-zero-note) | /* these are float values but not literals: */ inf, nan, or -inf | // these are float values but not literals: +Inf, NaN, *or* -Inf  // to get the float values: import "math"  math.Inf(1) math.Nan() math.Inf(-1) |
| [power](http://hyperpolyglot.org/c#power-note)               | #include <math.h>  pow(2.0, 3.0)                             | import "math"  math.Pow(2.0, 3.0)                            |
| [sqrt](http://hyperpolyglot.org/c#sqrt-note)                 | #include <math.h>  sqrt(2);                                  | include "math"  math.Sqrt(2)                                 |
| [sqrt -1](http://hyperpolyglot.org/c#sqrt-negative-one-note) | #include <math.h>  /* nan */ double x = sqrt(-1.0);          | import "math"  // NaN x := math.Sqrt(-2.0)  import "math/cmplx"  // (0+1.41421356i) z := cmplx.Sqrt(-2.0) |
| [transcendental functions](http://hyperpolyglot.org/c#transcendental-func-note) | #include <math.h>  exp log log2 log10 sin cos tan asin acos atan atan2 | include "math"  math.Exp math.Log math.Log2 math.Log10 math.Sin math.Cos math.Tan math.Asin math.Acos math.Atan math.Atan2 |
| [transcendental constants](http://hyperpolyglot.org/c#transcendental-const-note) | #include <math.h>  M_PI M_E                                  | import "math"  math.Pi Math.E                                |
| [float truncation](http://hyperpolyglot.org/c#float-truncation-note) | #include <math.h>   double d = 3.77;   long trunc = (long)d; long rnd = round(d); long flr = floorl(d); long cl = ceill(d); | include "math"  x = 3.77  trunc := int(x) *none* flr := int(math.Floor(x)) cl := int(math.Ceil(x)) |
| [absolute value](http://hyperpolyglot.org/c#absolute-val-note) | #include <math.h>  /* fabs() */  int i = abs(-7); float x = fabs(-7.77); | include "math"  *none* math.Abs(-7.77)                       |
| [complex type](http://hyperpolyglot.org/c#complex-type-note) | float complex *8 bytes* double complex *16 bytes* long double complex *32 bytes* | complex64 complex128                                         |
| [complex construction](http://hyperpolyglot.org/c#complex-construction-note) | #include <complex.h>  double complex z; z = 1.0 + 2.0 * I;  /* C11: */ double complex z = CMPLX(1.0, 2.0); | var z complex128 = 1.0 + 2.0i                                |
| [complex decomposition](http://hyperpolyglot.org/c#complex-decomposition-note) *real and imaginary component, argument, absolute value, conjugate* | #include <complex.h>  double x; double complex w;  x = creal(z); x = cimag(z); x = carg(z); x = cabs(z); w = conj(z); | import "math/cmplx"  var x float64 var w complex128  x = real(z) x = imag(z) x = cmplx.Phase(z) x = cmplx.Abs(z) w = cmplx.Conj(z) |
| [random number](http://hyperpolyglot.org/c#random-num-note) *uniform integer, uniform float* | /* lrand48 returns value in [0, 2**31 - 1]: */ long n = lrand48(() % 100;  /* Value in interval [0.0, 1.0): */ double x = drand48(); | import "math/rand"  n := rand.Intn(100) x := rand.Float64()  |
| [random seed](http://hyperpolyglot.org/c#random-seed-note)   | srand48(17);                                                 | import "math/rand"  rand.Seed(17)                            |
| [bit operators](http://hyperpolyglot.org/c#bit-op-note)      | << >> & \| ^ ~                                               | << >> & \| *none* ^                                          |
| [binary, octal, and hex literals](http://hyperpolyglot.org/c#binary-octal-hex-note) | *none* 052 0x2a                                              | *none* 052 0x2a                                              |
| [strings](http://hyperpolyglot.org/c#strings-note)           |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [string type](http://hyperpolyglot.org/c#str-type-note)      | char * wchar_t *  wchar_t *is typically 32 bits on Linux and 16 bits on Windows.* | // immutable: string  // mutable: []byte                     |
| [string literal](http://hyperpolyglot.org/c#str-literal-note) | /* string in initialized data segment: */ char *s = "hello"; wchar_t *ws = L"hello";  /* string in heap: */ char *s2 = strdup(s); wchar_t *ws2 = wcsdup(ws);  /* if strdup cannot allocate memory, it returns NULL and sets    errno to ENOMEM. */ | "hello"  // raw string literal: `hello`  // convert literal to mutable string: []byte("hello") |
| [newline in string literal](http://hyperpolyglot.org/c#newline-in-str-literal-note) | /* compiler concatenates literals    separated by whitespace: */ char *s = "first line\n"   "second line"; | // backquote literals only: let s := `first line second line` |
| [string escapes](http://hyperpolyglot.org/c#str-literal-esc-note) | \a \b \f \n \r \t \v \" \' \? \\ \*o* \*oo* \*ooo* \x*hh* \u*hhhh* \U*hhhhhhhh* | *Double quote literals only:*  \a \b \f \n \r \t \v \\ \" \*ooo* \x*hh* \u*hhhh* \U*hhhhhhhh* |
| [compare strings](http://hyperpolyglot.org/c#compare-str-note) | /* == and < compare memory addresses: */  strcmp("hello", "world") == 0 strcmp("hello", "world") < 0  wcscmp(L"hello", L"world") == 0 wcscmp(L"hello", L"world") < 0 | "hello" == "world" "hello" < "world"                         |
| [string to number](http://hyperpolyglot.org/c#str-to-num-note) | /* conversion functions:     strtol strtoll     strtoul strtoull     strtof strtod strtold */ #include <limits.h>  char *s = "101 dalmations"; char *rest; long n = strtol(s, &rest, 10);  if (n == 0 && errno == EINVAL)   printf("invalid input\n"); else if ((n == LONG_MAX \|\| n == LONG_MIN) && errno == ERANGE)   printf("overflow\n"); else   printf("%ld %s\n", n, rest);  /* wide string conversion functions:     wcstol wcstoll     wcstoul wcstoull     wcstof wcstod wcstold */ | import "strconv"  //2nd arg is base, 3rd arg is size of int in bits: i, _ := strconv.ParseInt("17", 10, 32)  // 2nd arg is size of float in bits: x, _ := strconv.ParseFloat("3.14", 32) |
| [number to string](http://hyperpolyglot.org/c#num-to-str-note) | long n = 1234;  char buf[100]; snprintf(buf, 100, "%ld", n);  wchar_t buf2[100]; swprintf(buf2, 100, L"%ld", n);  /* some format specifiers:     %d %ld %lld     %u %lu %llu     %.3f %.3e */ | import "strconv"  //3rd arg is precision after decimal point; // 4th arg is size of float in bits: strconv.FormatFloat(3.14, 'f', 4, 32)  // 2nd arg is base: strconv.FormatInt(7, 10) |
| [split](http://hyperpolyglot.org/c#split-note)               | /* strtok_r modifies 1st arg */ char *s = strdup("foo,bar baz"); char *sep = " ,"; char *tok, *last;  /* tok is never an empty string: */ for (tok = strtok_r(s, sep, &last);      tok;      tok = strtok_r(NULL, sep, &last))   printf("token: %s\n", tok);  /* also wcstok */ | import "strings"  s := "foo bar baz" parts := strings.Split(s, " ") |
| [join](http://hyperpolyglot.org/c#str-join-note)             | *none*                                                       | import "strings"  parts := []string{"foo", "bar", "baz"} s := strings.Join(parts, " ") |
| [concatenate](http://hyperpolyglot.org/c#str-concat-note)    | char *s1 = "hello"; char *s2 = " world"; size_t len = strlen(s1) + strlen(s2) + 1; char *s3 = (char *)calloc(len, sizeof *s3);  strcpy(s3, s1); strcat(s3, s2);  /* also wcscpy and wcscat */ | "hello" + " world"                                           |
| [replicate](http://hyperpolyglot.org/c#str-replicate-note)   | *none*                                                       | import "strings"  hbar := strings.Repeat("-", 80)            |
| [extract substring](http://hyperpolyglot.org/c#extract-substr-note) | char target[3]; char *source = "hello";  strncpy(target, source + 2, 2); target[2] = '\0';  /* also wcsncpy */ | "hello"[2:4]                                                 |
| [index of substring](http://hyperpolyglot.org/c#index-substr-note) | const char *s = "hello"; const char *p = strstr("hello", "ll"); size_t idx = p ? p - s : -1;  /* also wcsstr */ | import "strings"  // zero-based index; -1 if not found: strings.Index("hello", "ll") |
| [format string](http://hyperpolyglot.org/c#fmt-str-note)     | char buf[100]; snprintf(buf, 100, "%s: %d", "Spain", 7);  wchar_t buf2[100]; swprintf(buf2, 100, L"%S: %d", L"Spain", 7); | buf := fmt.Sprintf("%s: %d", "Spain", 7)                     |
| [translate case](http://hyperpolyglot.org/c#translate-case-note)  *to upper, to lower* | char *s = strdup("hello"); int i;  for (i=0; i < strlen(s); ++i)   s[i] = toupper(s[i]);  for (i=0; i < strlen(s); i++)   s[i] = tolower(s[i]);  /* also towupper and towlower */ | import "strings"  strings.ToUpper("hello") strings.ToLower("HELLO") |
| [trim](http://hyperpolyglot.org/c#trim-note) *both sides, on left, on right* | char *s = strdup(" lorem "); size_t i, j;  /* trim left */ for (i = 0; s[i] && isspace(s[i]); ++i); if (i)   for (size_t j = 0; j < strlen(s) - i + 1; ++j)     s[j] = s[j + i];  /* trim right */ for (i = strlen(s) - 1; s[i] && isspace(s[i]); i); s[i + 1] = '\0';  /* also iswspace */ | import "strings"  s := " lorem " strings.Trim(s, " ") strings.TrimLeft(s, " ") strings.TrimRight(s, " ") |
| [pad](http://hyperpolyglot.org/c#pad-note)                   | char buf[100];  /* pad right: */ snprintf(buf, 100, "%-10s", "hello"); /* pad left: */ snprintf(buf, 100, "%10s", "hello");  /* also swprintf */ | right_pad := fmt.Sprintf("%-10s\n", "hello") left_pad := fmt.Sprintf("%10s\n", "hello") |
| [length](http://hyperpolyglot.org/c#str-len-note)            | strlen("hello") wcslen(L"hello")                             | s := "αλφα"  char_length := 0 // iterate over characters, setting i to index and rune_val // to Unicode point. Bad bytes get code point 0xFFFD: for i, rune_val := range s {   fmt.Printf("%d %d\n", i, rune_val)   char_length += 1 }  fmt.Printf("bytes: %d chars: %d\n", len(s), char_length) |
| [character type](http://hyperpolyglot.org/c#char-type-note)  | char wchar_t                                                 | byte rune                                                    |
| [character literal](http://hyperpolyglot.org/c#char-literal-note) | 'A' L'A'                                                     | *none*                                                       |
| [character lookup](http://hyperpolyglot.org/c#char-lookup-note) | "lorem ipsum"[6] L"lorem ipsum"[6]                           | // 7th byte: "lorem ipsum"[6]  // 7th char: s := "αλφα βητα" var ch rune for i, rune_val := range s {   if i == 6 {     ch = rune_val   } } |
| [character index](http://hyperpolyglot.org/c#char-index-note) | char *s = "aaa bbb ccc"; char *p; size_t n;  p = strchr(s, ' '); if (p)   printf("first space at %ld\n", p - s); p = strrchr(s, ' '); if (p)   printf("last space at %ld\n", p - s);  n = strspn(s, "abc"); printf("first %ld chars in set\n", n); p = strpbrk(s, " ,:."); printf("first %ld chars not in set\n", n);  /* also: wcschr wcsrchr wcsspn wcspbrk */ |                                                              |
| [character tests](http://hyperpolyglot.org/c#char-tests-note) | #include <ctype.h> #include <wctype.h>  isascii(ch) isrune(ch) iscntrl(ch) isgraph(ch) isalpha(ch) isspace(ch) isupper(ch) islower(ch) isalnum(ch) isdigit(ch) isxdigit(ch) ispunct(ch)  /* also: iswascii, iswrune, ... */ | import "unicode"  unicode.IsControl(ch) unicode.IsGraphic(ch) unicode.IsLetter(ch) unicode.IsSpace(ch) unicode.IsUpper(ch) unicode.IsLower(ch) unicode.IsDigit(ch) unicode.IsPunct(ch) |
| [chr and ord](http://hyperpolyglot.org/c#chr-ord-note)       | /* Character types are integer types so no conversion is necessary. Use %c and %C to print a character like a string of length one. */ char ch = 'A'; wchar_t ch2 = L'A';  int i = ch + 7; int i2 = ch2 + 7;  wprintf(L"%c %d %C %d\n", ch, ch, ch2, ch2); | /* Character types are integer types so no conversion is necessary. Use %c to print a character like a string of length one. */  fmt.Printf("lambda: %c\n", 0x3bb) |
| [regular expressions](http://hyperpolyglot.org/c#regexes-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [metacharacters](http://hyperpolyglot.org/c#regex-metachar-note) | /* REG_BASIC: */ . [ ] \ * ^ $  /* REG_EXTENDED: */ . [ ] \ ( ) * + ? { } | ^ $ | . [ ] \ ( ) * + ? { } \| ^ $  *use raw string (i.e. backtick) literals to avoid having to escape backslashes.* |
| [character class abbrevations](http://hyperpolyglot.org/c#char-class-abbrev-note) | /* matches any character; does not match newline if    REG_NEWLINE is used: */ .  /* more character classes available in pcre library */ | . \d \D \s \S \w \W                                          |
| [anchors](http://hyperpolyglot.org/c#regex-anchors-note)     | /* match beginning and end of string; match beginning and    end of line if REG_NEWLINE is used: */ ^ $ | ^ $ \A \b \B \z                                              |
| [match test](http://hyperpolyglot.org/c#regex-test-note)     | #include <regex.h>  regex_t rx; int retval; char *pat = "1999"; char *s = "It's 1999";  /* Use REG_NOSUB if 4th arg to regexec() is NULL */ if (retval = regcomp(&rx, pat, REG_EXTENDED \| REG_NOSUB)) {   char buf[200];   regerror(retval, &rx, buf, 200);   fprintf(stderr, "regex error: %s\n", buf); } else {   if (regexec(&rx, s, 0, NULL, 0) == 0)     printf("Party!\n");   regfree(&rx); } | import "regexp"  var rx = regexp.MustCompile("1999") if (rx.MatchString("It's 1999.")) {   fmt.Println("Party!") } |
| [case insensitive match test](http://hyperpolyglot.org/c#case-insensitive-regex-note) | #include <regex.h>  regex_t rx; int retval; char *pat = "lorem"; char *s = "Lorem";  if (retval = regcomp(&rx, pat, REG_EXTENDED \| REG_ICASE)) {   char buf[200];   regerror(retval, &rx, buf, 200);   fprintf(stderr, "Regex error: %s\n", buf); } else {   if (regexec(&rx, s, 0, NULL, 0) == 0)     printf("case insensitive match\n");   regfree(&rx); } | import "regexp"  var rx = regexp.MustCompile("(?i)lorem") if (rx.MatchString("Lorem Ipsum")) {   fmt.Println("case insensitive match") } |
| [modifiers](http://hyperpolyglot.org/c#regex-modifiers-note) | /* bit flags used in 3rd arg of regcomp(): */ REG_BASIC REG_EXTENDED REG_ICASE REG_NOSUB REG_NEWLINE | // use (?i), (?m), ... to insert in regex: i m s U           |
| [substitution](http://hyperpolyglot.org/c#subst-note)        |                                                              | import "regexp"  s := "do re mi mi mi" var rx = regexp.MustCompile("mi") fmt.Println(rx.ReplaceAllString(s, "ma")) |
| [group capture](http://hyperpolyglot.org/c#group-capture-note) | #include <regex.h>  regex_t rx; int retval; char *pat = "([0-9]{4})-([0-9]{2})-([0-9]{2})"; char *s = "2010-06-03";  if (retval = regcomp(&rx, pat, REG_EXTENDED)) {   char buf[200];   regerror(retval, &rx, buf, 200);   fprintf(stderr, "Regex error: %s\n", buf); } else {   /* first match is entire pattern */   regmatch_t matches[4];   if (regexec(&rx, s, 4, matches, 0) == 0) {     char yr[5];     regmatch_t rm = matches[1];     /* rm_so and rm_eo contain index of start and end of        match; they are set to -1 if unused */     strncpy(yr, s + rm.rm_so, rm.rm_eo - rm.rm_so);     yr[5] = '\0';     printf("year is %s\n", yr);   }   regfree(&rx); } |                                                              |
| [dates and time](http://hyperpolyglot.org/c#dates-time-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [unix epoch type](http://hyperpolyglot.org/c#unix-epoch-type-note) | time_t                                                       | int64                                                        |
| [broken-down datetime type](http://hyperpolyglot.org/c#broken-down-datetime-type-note) | struct tm                                                    | Time                                                         |
| [current unix epoch](http://hyperpolyglot.org/c#current-unix-epoch-note) | time_t now;  if (time(&now) == -1)   perror("time failed");  | import "time"  t := time.Now().Unix()                        |
| [current datetime](http://hyperpolyglot.org/c#current-datetime-note) |                                                              | import "time"  dt := time.Now()                              |
| [broken-down datetime to unix epoch](http://hyperpolyglot.org/c#broken-down-datetime-to-unix-epoch-note) | /* use host local time as tz: */ time_t t = mktime(&dt);  /* use UTC as tz: */ time_t t2 = timegm(&dt2); | t := dt.Unix()                                               |
| [unix epoch to broken-down datetime](http://hyperpolyglot.org/c#unix-epoch-to-broken-down-datetime-note) | struct tm dt, dt2;  if (!localtime_r(&now, &dt))   perror("localtime_r failed");  /* UTC: */ if (!gmtime_r(&now, &dt2))   perror("gmtime_r failed"); | var t int64 = 1421929926 var ns int64 = 0 dt := time.Unix(t, ns) |
| [format datetime](http://hyperpolyglot.org/c#fmt-datetime-note) | char buf[100]; char *fmt = "%Y-%m-%d %H:%M:%S";  if (!strftime(buf, 100, fmt, &dt))   fputs("strftime failed\n", stderr); | layout := "2006-01-02 15:04:05"  fmt.Println(dt.Format(layout)) |
| [parse datetime](http://hyperpolyglot.org/c#parse-datetime-note) | char *s = "1999-09-10 23:30:00"; char *fmt = "%Y-%m-%d %H:%M:%S"; char *p = strptime(s, fmt, &dt3); if (!p)   fputs("strptime failed\n", stderr); | layout := "2006-01-02:15:04:05"  dt, err := time.Parse(layout, "1999-09-10 23:30:00") |
| [date subtraction](http://hyperpolyglot.org/c#date-subtraction-note) | /* use mktime for local; timegm for utc: */ double delta_sec = difftime(mktime(&dt), mktime(&dt2)); | var delta time.Duration  delta = dt.Sub(dt2)                 |
| [add duration](http://hyperpolyglot.org/c#add-duration-note) | dt.tm_sec += 1000; mktime(&dt);  dt.tm_hour += 1000; mktime(&dt);  dt.tm_mday += 1000; mktime(&dt); | dt2 := dt + 1000 * time.Second dt3 := dt + 1000 * time.Hour  |
| [date parts](http://hyperpolyglot.org/c#date-parts-note)     | int yr = dt.tm_year + 1900; int mo = dt.tm_mon + 1; int dy = dt.tm_mday; | yr := dt.Year() var mo time.Month = dt2.Month() dy := dt.Day() |
| [time parts](http://hyperpolyglot.org/c#time-parts-note)     | int hr = dt.tm_hour; int mi = dt.tm_min; int ss = dt.tm_sec; | hr := dt.Hour() mi := dt.Minute() ss := dt.Second()          |
| [build broken-down datetime](http://hyperpolyglot.org/c#build-datetime-note) | dt.tm_year = 1999 - 1900; dt.tm_mon = 9 - 1; dt.tm_mday = 10; dt.tm_hour = 23; dt.tm_min = 30; dt.tm_sec = 0; dt.tm_isdst = 1; dt.tm_gmtoff = -7 * 60 * 60;  if (mktime(&dt) == -1)   fputs("mktime failed\n", stderr); | import "time"  yr := 1999 var mo time.Month = 9 dy, hr, mi, ss, ns := 10, 23, 30, 0, 0 loc, _ := time.LoadLocation("Local")  dt := time.Date(yr, mo, dy, hr, mi, ss, ns, loc) |
| [local time zone determination](http://hyperpolyglot.org/c#local-tmz-determination-note) | *On a Unix system, the local time zone is stored in /etc/localtime. A process can have a different local time zone by setting the TZ environment variable.* |                                                              |
| [time zone info](http://hyperpolyglot.org/c#tmz-info-note) *name and utc offset in hours* | *offset abbreviation:* dt.tm_zone  *UTC offset in hours:* dt.tm_gmtoff / 3600.0 | name, offset_sec := dt.Zone()  *offset abbreviation:* name  *UTC offset in hours:* offset_sec / 3600.0 |
| [daylight savings test](http://hyperpolyglot.org/c#daylight-savings-test-note) | dt.tm_isdst                                                  |                                                              |
| [microseconds](http://hyperpolyglot.org/c#microseconds-note) | #include <sys/time.h>  struct timeval t;  if (gettimeofday(&t, NULL) == -1)   perror("gettimeofday failed"); else   printf("epoch: %lu usec: %u\n", t.tv_sec, t.tv_usec); | dt.Nanosecond() / 1000                                       |
| [fixed-length arrays](http://hyperpolyglot.org/c#fixed-length-arrays-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [declare](http://hyperpolyglot.org/c#declare-array-note)     | int a[10];                                                   | // values are zero-initialized: var a [10]int                |
| [allocate on stack](http://hyperpolyglot.org/c#allocate-array-on-stack-note) | /* contents of memory undefined: */ int a[10];               | *compiler decides location in memory*                        |
| [allocate on heap](http://hyperpolyglot.org/c#allocate-array-on-heap-note) | #include <stdlib.h>  /* memory zero-initialized: */ int *a = calloc(10, sizeof *a); | *compiler decides location in memory*                        |
| [free heap](http://hyperpolyglot.org/c#free-array-on-heap-note) | free(a);                                                     | *none; garbage collected*                                    |
| [literal](http://hyperpolyglot.org/c#array-literal-note)     | int a[] = {1, 2, 3};                                         | *none*                                                       |
| [size](http://hyperpolyglot.org/c#array-size-note)           | sizeof(a) / sizeof(a[0])                                     | len(a)                                                       |
| [lookup](http://hyperpolyglot.org/c#array-lookup-note)       | a[0]                                                         | a[0]                                                         |
| [update](http://hyperpolyglot.org/c#array-update-note)       | a[0] = 4;                                                    | a[0] = 4                                                     |
| [out-of-bounds behavior](http://hyperpolyglot.org/c#array-out-of-bounds-note) | *undefined, possible SIGSEGV*                                | panic: index out of range  *if compiler detects a problem the code won't compile* |
| [element index](http://hyperpolyglot.org/c#array-element-index-note) | char *a[3] = {"foo", "bar", "baz"}; int loc = -1, i;  for (i = 0; i < 3; ++i) {   if (strcmp("bar", a[i]) == 0) {     loc = i;     break;   } } | var a [3]string a[0] = "foo" a[1] = "bar" a[2] = "baz" loc := -1  for i, val := range a {   if val == "bar" {     loc = i   } } |
| [copy](http://hyperpolyglot.org/c#copy-array-note)           | int a[3] = {1, 2, 3}; int b[3];  memcpy(b, a, sizeof(a));    | a := []int{1, 2, 3}  a2 := a // also sets a[0] to 4: a2[0] = 4  a3 := make([]int, len(a)) copy(a3, a) // a[0] is unchanged: a3[0] = 5 |
| [iterate over elements](http://hyperpolyglot.org/c#iterate-over-array-note) | int a[10];  for (i = 0; i < 10; ++i ) {   a[i] = i * i; }    | var a [10]int  for i, _ := range a {   a[i] = i * i } for _, num := range a {   fmt.Printf("%d\n", num) } |
| [sort](http://hyperpolyglot.org/c#sort-array-note)           | int compare(const void *a, const void *b) {   if (*(int *)a < *(int *)b) {     return -1;   }     else if (*(int *)a == *(int *)b) {     return 0;   }   else {     return 1;   } }  int a[5] = {6, 8, 10, 9, 7};  /* 2nd arg is array length; 3rd arg is element size */ qsort(a, 5, sizeof (int), &compare); | *convert to resizable array*                                 |
| [resizable arrays](http://hyperpolyglot.org/c#resizable-arrays-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [declare](http://hyperpolyglot.org/c#declare-resizable-array-note) |                                                              | // Resizable arrays are called slices. // To declare a slice instead of a fixed-length array, // omit the length from the type: var a []int // slice of length 5; capacity 10: a = make([]int, 5, 10) |
| [literal](http://hyperpolyglot.org/c#resizable-array-literal-note) |                                                              | a := []int{1, 2, 3}                                          |
| [size](http://hyperpolyglot.org/c#resizable-array-size-note) |                                                              | len(a)  // number of elements that can be stored in allocated memory; // runtime reallocates when needed: cap(a) |
| [lookup](http://hyperpolyglot.org/c#resizable-array-lookup-note) |                                                              | a[0]                                                         |
| [update](http://hyperpolyglot.org/c#resizable-array-update-note) |                                                              | a[0] = 4                                                     |
| [resizable to fixed array](http://hyperpolyglot.org/c#resizable-to-fixed-note) |                                                              | resizable := []int{1, 2, 3} var fixed [3]int copy(fixed[:], resizable) |
| [fixed to resizable array](http://hyperpolyglot.org/c#fixed-to-resizable-note) |                                                              | var resizable2 []int resizable2 = fixed[:]                   |
| [out-of-bounds behavior](http://hyperpolyglot.org/c#resizable-array-out-of-bounds-note) |                                                              | *Both lookups and updates cause panics when out-of-bounds*   |
| [element index](http://hyperpolyglot.org/c#resizable-array-element-index-note) |                                                              | a := []string{"foo", "bar", "baz"} loc := -1  for i, val := range a {   if val == "bar" {     loc = i   } } |
| [slice](http://hyperpolyglot.org/c#slice-resizable-array-note) |                                                              | a := []string{"a", "b", "c", "d", "e"}  // {"c", "d"}: a2 := a[2:4] |
| [slice to end](http://hyperpolyglot.org/c#slice-resizable-array-to-end-note) |                                                              | a := []string{"a", "b", "c", "d", "e"}  // {"c", "d", "e"}: a2 := a[2:] |
| [manipulate back](http://hyperpolyglot.org/c#resizable-array-back-note) |                                                              | a := []int{1, 2, 3}  a = append(a, 4) num := a[len(a) - 1] a = a[:len(a) - 1] |
| [manipulate front](http://hyperpolyglot.org/c#resizable-array-front-note) |                                                              | a := []int{1, 2, 3}  a = append([]int{0}, a...) num := a[0] a = a[1:] |
| [concatenate](http://hyperpolyglot.org/c#concatenate-resizable-array-note) |                                                              | a := []int{1, 2, 3} a2 := []int{4, 5, 6} a3 := append(a, a2...) |
| [copy](http://hyperpolyglot.org/c#copy-resizable-array-note) |                                                              | a := []int{1, 2, 3}  a2 := a // also sets a[0] to 4: a2[0] = 4  a3 := make([]int, len(a)) copy(a3, a) // a[0] is unchanged: a3[0] = 5 |
| [iterate over elements](http://hyperpolyglot.org/c#iterate-over-resizable-array-note) |                                                              | a := []string{"do", "re", "mi"} for _, s := range(a) {   fmt.Printf("value: %s\n", s) } |
| [iterate over indices and elements](http://hyperpolyglot.org/c#iterate-indices-elem-note) |                                                              | a := []string{"do", "re", "mi"} for i, s := range(a) {   fmt.Printf("value at %d: %s\n", i, s) } |
| [reverse](http://hyperpolyglot.org/c#reverse-resizable-array-note) |                                                              | import "sort"  a := []int{1, 2, 3} sort.Sort(sort.Reverse(sort.IntSlice(a))) |
| [sort](http://hyperpolyglot.org/c#sort-resizable-array-note) |                                                              | unsortedInts := []int{3, 1, 4, 2} sortedInts := sort.IntSlice(unsortedInts) sort.Sort(sortedInts) // sortedInts is now []int{1, 2, 3, 4}  floats := []float64{3.0, 1.0, 4.0, 2.0} sort.Float64s(floats) // floats is now []float64{1.0, 2.0, 3.0, 4.0}  strs := []string{"b", "a", "d", "c"} sort.Strings(strs) // strs is now []string{"a", "b", "c", "d"} |
| [dictionaries](http://hyperpolyglot.org/c#dictionaries-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [declare](http://hyperpolyglot.org/c#declare-dict-note)      |                                                              | d := make(map[string]int)                                    |
| [literal](http://hyperpolyglot.org/c#dict-literal-note)      |                                                              | d := map[string]int {"t": 1, "f": 0}                         |
| [size](http://hyperpolyglot.org/c#dict-size-note)            |                                                              | len(d)                                                       |
| [lookup](http://hyperpolyglot.org/c#dict-lookup-note)        |                                                              | d["t"]                                                       |
| [update](http://hyperpolyglot.org/c#dict-update-note)        |                                                              | d["t"] = 2                                                   |
| [missing key behavior](http://hyperpolyglot.org/c#dict-missing-key-note) |                                                              | *returns zero value for value type*                          |
| [is key present](http://hyperpolyglot.org/c#dict-is-key-present-note) |                                                              | // If key not present, val will contain // zero value for type and ok will contain false: val, ok = d["y"]] |
| [delete](http://hyperpolyglot.org/c#dict-delete-note)        |                                                              | delete(d, "f")                                               |
| [iterate](http://hyperpolyglot.org/c#dict-iter-note)         |                                                              | for k, v := range d {   fmt.Printf("%s: %d\n", k, v) }       |
| [functions](http://hyperpolyglot.org/c#functions-note)       |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [define function](http://hyperpolyglot.org/c#def-func-note)  | int add(int n, int m) {   return n + m; }                    | func add(n int, m int) int {   return n + m }  // parameters can share type declaration: func add(n, m int) int {   return n + m } |
| [invoke function](http://hyperpolyglot.org/c#invoke-func-note) | add(3, 7)                                                    | add(3, 7)                                                    |
| [forward declaration of function](http://hyperpolyglot.org/c#forward-decl-func-note) | float add(float x, float y);  /* if a function invocation is encountered before a   declaration or a definition, the arguments and the   return value are assumed to have type 'int' */ printf("%f\n", add(2.2, 3.5));  float add(float x, float y) {   return x + y; } | // function can be invoked before definition fmt.Printf("%f\n", add(2.2, 3.5))  func add(n float32, m float32) float32 {   return n + m } |
| [overload function](http://hyperpolyglot.org/c#overload-func-note) | *not permitted*                                              | *not permitted*                                              |
| [nest function](http://hyperpolyglot.org/c#nest-func-note)   | *not permitted*                                              | *the normal function declaration syntax cannot be nested, but see anonymous functions below* |
| [default value for parameter](http://hyperpolyglot.org/c#default-val-param-note) | *none*                                                       | *none*                                                       |
| [variable number of arguments](http://hyperpolyglot.org/c#variable-num-arg-note) | #include <stdarg.h>  char* concat(int cnt, ...) {    int i, len;   va_list ap;   char *retval, *arg;    va_start(ap, cnt);   for (i = 0, len = 0; i < cnt; i++) {     len += strlen(va_arg(ap, char*));   }   va_end(ap);    retval = calloc(len + 1, sizeof *retval);    va_start(ap, cnt);   for (i = 0, len = 0; i < cnt; i++) {     arg = va_arg(ap, char*);     strcpy(retval + len, arg);     len += strlen(arg);   }   va_end(ap);    return retval; }  char *s = concat(4, "Hello", ", ", "World", "!"); | func concat(strs ...string) string {   var ret = ""   for _, str := range strs {     ret += str   }    return ret } |
| [named parameters](http://hyperpolyglot.org/c#named-param-note) | *none*                                                       | *none*                                                       |
| [pass by value](http://hyperpolyglot.org/c#pass-by-val-note) | void print_integer(int i) {   printf("integer: %d\n", i); }  int i = 7; print_integer(i); | func print_integer(i int) {  fmt.Printf("integer: %d\n", i) }  i := 7 print_integer(i) |
| [pass by address](http://hyperpolyglot.org/c#pass-by-addr-note) | void print_iptr(int *i) {   printf("integer: %d\n", *i); }  int i = 7;  print_iptr(&i); | func print_iptr(i *int) {   fmt.Printf("integer: %d\n", *i); }  i := 7 print_iptr(&i) |
| [return value](http://hyperpolyglot.org/c#retval-note)       | return *arg*                                                 | return *arg. If return values have names and no arguments are provided to* return *the values assigned to the return variables are used.* |
| [no return value](http://hyperpolyglot.org/c#no-retval-note) | /* declare function void: */ void print_err(char *msg) {   fprintf(stderr, msg); } | import "os"  func print_err(msg string) {   os.Stderr.WriteString(msg)   os.Stderr.WriteString("\n") } |
| [multiple return values](http://hyperpolyglot.org/c#multiple-retval-note) | *not permitted*                                              | func divmod(m, n int) (int, int) {   return m / n, m % n }  q, r := divmod(7, 3) |
| [named return values](http://hyperpolyglot.org/c#named-retval-note) | *none*                                                       | func divmod(m, n int) (q, r int) {   q = m / n   r = m % n   return }  q, r := divmod(7, 3) |
| [execute on return](http://hyperpolyglot.org/c#exec-on-return-note) |                                                              | import "os"  // prints "x is 7" func x_is_7() {   x := 7   defer fmt.Println(x)   x = 8   defer os.Stdout.WriteString("x is ") } |
| [anonymous function literal](http://hyperpolyglot.org/c#anonymous-func-literal-note) | *none*                                                       | square := func(i int) int {   return i * i }                 |
| [invoke anonymous function](http://hyperpolyglot.org/c#invoke-anonymous-func-note) | *none*                                                       | square(7)                                                    |
| [function with private state](http://hyperpolyglot.org/c#func-private-state-note) | int counter() {   static int n = 0;    return ++n; }         | *none*                                                       |
| [closure](http://hyperpolyglot.org/c#closure-note)           | *none*                                                       | func make_counter() func() int {   i := 0   return func() int {     i += 1     return i   } }  counter := make_counter() fmt.Printf("%d\n", counter()) |
| [function as value](http://hyperpolyglot.org/c#func-as-val-note) | int add(int m, int n) {   return m + n; }  /* a function cannot be stored in a variable, but   its address can */ int (* fp)(int, int) = &add;  printf("1 + 2: %d\n", (*fp)(1, 2)); | *Cannot get the address of a named function.*                |
| [execution control](http://hyperpolyglot.org/c#execution-control-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [if](http://hyperpolyglot.org/c#if-note)                     | int signum;  if (i > 0) {   signum = 1; } else if (i == 0) {   signum = 0; } else {   signum = -1; } | var signum int  if x > 0 {   signum = 1 } else if x == 0 {   signum = 0 } else {   signum = -1 } |
| [switch](http://hyperpolyglot.org/c#switch-note)             | /* switch expression must be an integer */  switch (i) { case 0: case 1:   printf("i is boolean\n");   break; default:   printf("i is not a boolean\n");   break; }  /* use "break" to prevent falling through */ | // switch expression can have any type  switch i { case 0, 1:   fmt.Println("i is boolean") default:   fmt.Println("i is not a boolean") }  // use "fallthrough" to fall through |
| [while](http://hyperpolyglot.org/c#while-note)               | int i = 0;  while (i < 10) {   ++i; }                        | i := 0  for i < 10 {   i++ }                                 |
| [for](http://hyperpolyglot.org/c#for-note)                   | int i, n;  for (i = 1, n = 1; i <= 10; ++i) {   n *= i; }    | var i, n int  // Initialization and afterthought must be single // statements; there is no comma operator. n = 1 for i = 1; i <= 10; i++ {   n *= i; } |
| [for with local scope](http://hyperpolyglot.org/c#for-local-scope-note) | *none*                                                       | n := 1  for i := 1; i <= 10; i++ {   n *= i; }  // i is no longer in scope |
| [infinite loop](http://hyperpolyglot.org/c#infinite-loop-note) | for (;;) {   /* code */ }  while (1) {   /* code */ }        | for {   // code }                                            |
| [break](http://hyperpolyglot.org/c#break-note)               | break                                                        | break                                                        |
| [break from nested loops](http://hyperpolyglot.org/c#break-from-nested-loops-note) | *use goto or flag variable*                                  | var a, b int  Outer:   for a = 1; ; a++ {     for b = 1; b < a; b++ {       c := int(math.Sqrt(float64(a * a + b * b)))       if c * c == a * a + b * b {         break Outer       }     }   } |
| [continue](http://hyperpolyglot.org/c#continue-note)         | continue                                                     | continue                                                     |
| [single statement branches and loops](http://hyperpolyglot.org/c#single-stmt-branch-loop-note) | while (n % 17 != 0)   ++n;  if (n < 0)   printf("negative\n"); | // braces are mandatory: if n < 0 {   fmt.Println("negative") } |
| [dangling else](http://hyperpolyglot.org/c#dangling-else-note) | int a = 1, b = -3, c;  /* indentation shows how ambiguity is resolved */ if (a > 0)   if (b > 0)     c = 1;   else     c = 2;  /* gcc warns about dangling else; -Werror turns warnings into errors */ | *no ambiguity*                                               |
| [goto](http://hyperpolyglot.org/c#goto-note)                 | if (err) {     goto cleanup;   }    /* code */  cleanup:   printf("cleaning up...\n"); | if err {     goto Cleanup   }    // code  Cleanup:   fmt.Println("cleaning up...") |
| [longjump](http://hyperpolyglot.org/c#longjmp-note)          | #include <setjmp.h>  void callee(jmp_buf env) {   longjmp(env, 1);   /* unreachable */ }  void caller() {   jmp_buf env;    switch (setjmp(env)) {   case 0:     callee(env);     /* unreachable */     break;   case 1:     printf("returned from callee\n");     break;   default:     printf("unexpected setjump value\n");   } } | *none*                                                       |
| [finally block](http://hyperpolyglot.org/c#finally-block-note) | *none*                                                       | *none, but see* "execute on return"                          |
| [concurrency](http://hyperpolyglot.org/c#concurrency-note)   |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [sleep](http://hyperpolyglot.org/c#sleep-note)               | #include <unistd.h>  /* seconds */ int retval = sleep(10); if (retval != 0) {   printf("interupted with %d s to go", retval); }  /* microseconds */ if (usleep(10000)) {   perror("usleep failed"); } | dur := time.Duration(10 * time.Second) time.Sleep(dur)  dur2 := time.Duration(10000 * time.Microsecond) time.Sleep(dur2) |
| [timeout](http://hyperpolyglot.org/c#timeout-note)           |                                                              |                                                              |
| [start thread](http://hyperpolyglot.org/c#start-thread-note) | #include <pthread.h>  typedef struct {   int id; } payload;  void* thread(void* arg) {   payload* pl = (payload*)arg;   printf("the value is %d\n", pl->id); }  pthread_t thr; payload pl = {3};  if (pthread_create(&thr, NULL, &thread, (void*)&pl)) {   printf("failed to create thead\n");   exit(1); } |                                                              |
| [terminate current thread](http://hyperpolyglot.org/c#terminate-current-thread-note) | #include <pthread.h>  payload pl = {7};  pthread_exit((void*)&pl); |                                                              |
| [terminate other thread](http://hyperpolyglot.org/c#terminate-other-thread-note) | #include <pthread>  pthread_t thr; payload pl = {3};  if (pthread_create(&thr, NULL, &thread, (void*)&pl)) {   printf("failed to create thead\n");   exit(1); }  sleep(5);  if (pthread_cancel(thr)) {   printf("failed to cancel thread\n");   exit (1); } |                                                              |
| [list threads](http://hyperpolyglot.org/c#list-threads-note) | *no portable way*                                            |                                                              |
| [wait on thread](http://hyperpolyglot.org/c#wait-on-thread-note) |                                                              |                                                              |
| [lock](http://hyperpolyglot.org/c#lock-note)                 |                                                              |                                                              |
| [create message queue](http://hyperpolyglot.org/c#create-message-queue-note) |                                                              |                                                              |
| [send message](http://hyperpolyglot.org/c#send-msg-note)     |                                                              |                                                              |
| [receive message](http://hyperpolyglot.org/c#receive-msg-note) |                                                              |                                                              |
| [file handles](http://hyperpolyglot.org/c#file-handles-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [standard file handles](http://hyperpolyglot.org/c#std-file-handles-note) | stdin stdout stderr                                          | import "os"  os.Stdin os.Stdout os.Stderr                    |
| [read line from stdin](http://hyperpolyglot.org/c#read-line-stdin-note) | char *line = NULL; size_t cap = 0; ssize_t len;  /* if line is not NULL, it should be memory allocated by    malloc and the size should be in cap. If size is not    sufficient getline will call realloc on line */ len = getline(&line, &cap, stdin);  if (len == -1) {   if (ferror(stdin)) {     perror("getline err");   }   else if (feof(stdin)) {     fprintf(stderr, "end of file\n");   } } else {    /* use line here */    free(line); } | import "bufio" import "os"  var line string var err error  b := bufio.NewReader(os.Stdin)  line, err = b.ReadString('\n')  if err != nil {   os.Stderr.WriteString("error!") } else {   // use line here } |
| [write line to stdout](http://hyperpolyglot.org/c#write-line-stdout-note) | /* returns EOF on error */ int retval = puts("Hello, World!"); | import "os"  os.Stdout.WriteString("Hello, World!\n")        |
| [write formatted string to stdout](http://hyperpolyglot.org/c#printf-note) | printf("count: %d\n", 7); wprintf(L"count: %d\n", 7);        | fmt.Printf("count: %d\n", 7)                                 |
| [open file for reading](http://hyperpolyglot.org/c#open-file-note) | /* returns NULL on error */ FILE *f = fopen("/etc/hosts", "r"); | import "os"  raw, err := os.Open("/etc/hosts") if err == nil {   f := bufio.NewReader(raw) } |
| [open file for writing](http://hyperpolyglot.org/c#open-file-write-note) | /* returns NULL on error */ FILE *f = fopen("/tmp/test", "w"); | import "os"  perms := os.O_RDWR \| os.O_CREATE f, err := os.OpenFile("/tmp/test", perms, 0644) |
| [open file for appending](http://hyperpolyglot.org/c#open-file-append-note) | /* returns NULL on error */ FILE *f = fopen("/tmp/err.log", "a"); | import "os"  perms := os.O_RDWR \| os.O_CREATE \| os.O_APPEND f, err := os.OpenFile("/tmp/test", perms, 0644) |
| [close file](http://hyperpolyglot.org/c#close-file-note)     | /* returns EOF on error */ int retval = fclose(f);           | err := f.Close()                                             |
| [i/o errors](http://hyperpolyglot.org/c#io-err-note)         | *Functions return values such as* EOF, NULL, *or* -1 *to indicate error. Some functions return the value of* errno. *In some cases errors are not distinguished from end-of-file. The functions* ferror() *and* feof() *can be used to test a file handle.The type of error is stored in* errno. strerror(errno) *or the thread safe*strerror_r(errno, buf, buflen) *convert the errors code to a string and*perror() *writes its argument to* stderr *with* sterror(errno). |                                                              |
| [read line](http://hyperpolyglot.org/c#read-line-note)       | char line[BUFSIZ];  if (fgets(line, BUFSIZ, f) == NULL) {   if (ferror(stdin)) {     perror("getline err");   }   else if (feof(stdin)) {     fprintf(stderr, "end of file\n");   }  } else {   if ('\n' == line[strlen(line) - 1]) {      /* use line here */  } else {     fprintf(stderr, "long line truncated\n"); } |                                                              |
| [iterate over file by line](http://hyperpolyglot.org/c#file-line-iterate-note) |                                                              |                                                              |
| [read file into array of strings](http://hyperpolyglot.org/c#read-file-array-note) |                                                              |                                                              |
| [read file into string](http://hyperpolyglot.org/c#read-file-str-note) |                                                              |                                                              |
| [write string](http://hyperpolyglot.org/c#write-str-note)    | /* returns EOF on error */ int retval = fputs("Hello, World!", f); | bytes_written, err := f.WriteString("Hello, World!")  bytes_written, err := f.Write(byte[]("Hello, World!")) |
| [write line](http://hyperpolyglot.org/c#write-line-note)     | /* returns EOF on error */ int retval = fputs("Hello, World!\n", f); | bytes_written, err := f.WriteString("Hello, World!\n")  bytes_written, err := f.Write(byte[]("Hello, World!\n")) |
| [flush file handle](http://hyperpolyglot.org/c#flush-note)   | if (fflush(f) == EOF) {   perror("fflush failed"); }         | err := f.Sync()                                              |
| [end-of-file test](http://hyperpolyglot.org/c#eof-test-note) | feof(f)                                                      |                                                              |
| [get and set file handle position](http://hyperpolyglot.org/c#seek-note) | long pos; if ((pos = ftell(f)) == -1) {   perror("ftell failed"); }  /* 3rd arg can also be SEEK_CUR or SEEK_END */ if (fseek(f, 0, SEEK_SET) == -1) {   perror("fseek failed"); } |                                                              |
| [open unused file](http://hyperpolyglot.org/c#tmp-file-note) | #include <limits.h>  /* PATH_MAX */ #include <unistd.h>  char buf[PATH_MAX];  strcpy(buf, "/tmp/foo.XXXXXX");  /* terminal Xs will be replaced: */ int fd = mkstemp(buf);  if (fd != -1) {   FILE *f = fdopen(fd, "w");    if (NULL == f) {     perror("fdopen failed");   } else {     /* use f */   }  } else {   perror("mkstemp failed"); } |                                                              |
| [files](http://hyperpolyglot.org/c#files-note)               |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [file test, regular file test](http://hyperpolyglot.org/c#file-test-note) | #include <sys/stat.h> #include <unistd.h>  /* access() */  struct stat buf;  if (access("/tmp/foo", F_OK) >= 0) {   /* file exists */ }  if (stat("/tmp/foo", &buf) != 0) {   perror("stat failed"); } else if (S_ISREG(buf.st_mode)) {   /* file is regular */ } | import "os"  fi, err := os.Stat("/tmp/foo") if os.IsNotExist(err) {   fmt.Printf("Does not exit\n") } else {   fmt.Printf("Exists\n")   fm := fi.Mode()   if fm.IsRegular() {     fmt.Printf("Is Regular")   } else {     fmt.Printf("Is Not Regular")   } } |
| [file size](http://hyperpolyglot.org/c#file-size-note)       | #include <sys/stat.h>  struct stat buf;  if (stat("/tmp/foo", &buf) != 0) {   perror("stat failed"); } else {   printf("size: %llu\n", buf.st_size); } | fi.Size()                                                    |
| [is file readable, writable, executable](http://hyperpolyglot.org/c#readable-writable-executable-note) | #include <unistd.h>  if (access("/etc/hosts", R_OK) != 0) {   printf("not readable\n"); } if (access("/etc/hosts", W_OK) != 0) {   printf("not writable\n"); } if (access("/etc/hosts", X_OK) != 0) {   printf("not executable\n"); } |                                                              |
| [set file permissions](http://hyperpolyglot.org/c#chmod-note) | #include <sys/stat.h>  if (chmod("/tmp/foo", 0755) == -1) {   perror("chmod failed"); } | import "os"  err := os.Chmod("/tmp/foo", 0755) if err != nil {   fmt.Printf("Chmod failed\n") } |
| [last modification time](http://hyperpolyglot.org/c#last-modification-time-note) |                                                              |                                                              |
| [copy file, remove file, rename file](http://hyperpolyglot.org/c#file-cp-rm-mv-note) | /* no copy function in standard library */  if (remove("/tmp/foo")) {   perror("remove failed"); }  if (rename("/tmp/bar", "/tmp/foo")) {   perror("rename failed"); } | import "os"  // no copy function in standard library  err := os.Remove("/tmp/foo") if err != nil {   fmt.Printf("Remove failed: %s\n", err) }  err2 := os.Rename("/tmp/bar", "/tmp/foo") if err2 != nil {   fmt.Printf("Rename failed: %s\n", err2) } |
| [create symlink, symlink test, readlink](http://hyperpolyglot.org/c#symlink-note) | #include <limits.h>  /* PATH_MAX */ #include <sys/stat.h> #include <unistd.h>  if (symlink("/etc/hosts", "/tmp/hosts") == -1) {   perror("symlink failed"); }  struct stat sbuf;  if (stat("/tmp/hosts", &buf) != 0) {   perror("stat failed"); } else if (S_ISLNK(buf.st_mode)) {   /* file is symlink */ }  char pbuf[PATH_MAX + 1];  ssize_t size = readlink("/tmp/hosts", pbuf, PATH_MAX);  if (size >= 0 ) {   pbuf[size] = 0;   /* pbuf now contains null-terminated string      with target path */ } | import "os"  err := os.Symlink("/etc/hosts", "/tmp/hosts") if err != nil {   fmt.Printf("Symlink failed: %s\n", err) }  fi, err2 := os.Lstat("/tmp/hosts") if err2 == nil {   fm := fi.Mode()   if fm & os.ModeSymlink != 0 {     fmt.Println("File is a Symlink")   } } else {   fmt.Printf("Lstat failed: %s\n", err2) }  s, err3 := os.Readlink("/tmp/hosts") if err3 != nil {   fmt.Printf("Readlink failed: %s\n", err3) } else {   fmt.Printf("Link target: %s\n", s) } |
| [generate unused file name](http://hyperpolyglot.org/c#unused-file-name-note) | /* if first argument is NULL, path is in system temp    directory. Caller should free() return value. */ char *path = tempnam("/tmp", "foo"); | import "io/ioutil"  // Uses system tmp dir if 1st arg is empty string: f, err := ioutil.TempFile("/tmp", "foo") if err == nil {   fmt.Printf("writing to: %s\n", f.Name())   f.WriteString("foo content") } |
| [file formats](http://hyperpolyglot.org/c#file-fmt-note)     |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [parse json](http://hyperpolyglot.org/c#parse-json-note)     |                                                              | import "encoding/json"  type TruthTable struct {   T int `json:T`   F int `json:F` }  bytes := []byte(‘{"T": 1, "F": 0}`) var truthTable TruthTable err := json.Unmarshal(bytes, &truthTable) |
| [generate json](http://hyperpolyglot.org/c#generate-json-note) |                                                              | import "encoding/json"  type TruthTable struct {   T int `json:T`   F int `json:F` }  truthTable := TruthTable{T: 1, F: 0} bytes, err := json.Marshal(truthTable) |
| [directories](http://hyperpolyglot.org/c#directories-note)   |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [working directory](http://hyperpolyglot.org/c#working-dir-note) |                                                              | import "os"  dir, err := os.Getwd() if err != nil {   os.Stderr.WriteString("Gtwd failed\n") } else {   fmt.Printf("pwd: %s\n", dir) }  err2 := os.Chdir("/tmp") if err2 != nil {   os.Stderr.WriteString("Chdir failed\n"); } |
| [build pathname](http://hyperpolyglot.org/c#build-pathname-note) |                                                              | import "path"  pathname := path.Join("/etc", "hosts") fmt.Printf("path: %s\n", pathname) |
| [dirname and basename](http://hyperpolyglot.org/c#dirname-basename-note) | #include <libgen.h>  char *s1 = strdup("/etc/hosts"); char *s2 = strdup("/etc/hosts"); /* Check whether s1 or s2 are NULL. */  /* Some implementations return pointers to statically allocated    memory which is overwritten by subsequent calls;    others modify the input string. */ char *s3 = dirname(s1); char *s4 = basename(s2); | import "path"  path.Dir("/etc/hosts") path.Base("/etc/hosts") |
| [absolute pathname](http://hyperpolyglot.org/c#absolute-pathname-note) | char *s;  if ((s = realpath("..", NULL)) == NULL) {   perror("realpath failed"); } else {   /* use s */ } |                                                              |
| [iterate over directory by file](http://hyperpolyglot.org/c#dir-iterate-note) | #include <dirent.h>  DIR *dir = opendir("/etc"); struct dirent *de;  while (de = readdir(dir)) {   printf("%s\n", de->d_name); }  closedir(dir); | import "io/ioutil"  a, err := ioutil.ReadDir("/etc") if err == nil {   for _, fi := range a {     fmt.Printf("name: %s\n", fi.Name())   } } |
| [glob paths](http://hyperpolyglot.org/c#glob-note)           | #include <glob.h>  glob_t pglob; int i;  glob("/etc/*", 0, NULL, &pglob);  for (i = 0; i < pglob.gl_pathc; ++i) {   printf("%s\n", pglob.gl_pathv[i]); }  globfree(&pglob); | import "path/filepath"  a, err := filepath.Glob("/etc/*") if err == nil {   for _, path := range(a) {     fmt.Printf("path: %s\n", path)   } } |
| [make directory](http://hyperpolyglot.org/c#mkdir-note)      | #include <sys/stat.h>  if (mkdir("/tmp/foo")) {   fprintf(stderr, "mkdir err: %s\n", strerror(errno)); } | err := os.Mkdir("/tmp/foo", 0775) if err != nil {   fmt.Printf("Mkdir failed: %s\n", err) } |
| [recursive copy](http://hyperpolyglot.org/c#recursive-cp-note) |                                                              |                                                              |
| [remove empty directory](http://hyperpolyglot.org/c#rmdir-note) | #include <unistd.h>  if (rmdir("/tmp/foo") == -1) {   perror("rmdir failed"); } | err := os.Remove("/tmp/foo") if err != nil {   fmt.Printf("Remove failed: %s", err) } |
| [remove directory and contents](http://hyperpolyglot.org/c#rm-rf-note) |                                                              | err := os.RemoveAll("/tmp/foo") if err != nil {   fmt.Printf("RemoveAll failed: %s", err) } |
| [directory test](http://hyperpolyglot.org/c#dir-test-note)   | #include <sys/stat.h>  struct stat buf;  if (stat("/tmp/foo", &buf) != 0) {   perror("stat failed"); } else if (S_ISDIR(buf.st_mode)) {   /* file is directory */ } |                                                              |
| [generate unused directory](http://hyperpolyglot.org/c#unused-dir-note) | #include <limits.h>  char buf[PATH_MAX];  strcpy(buf, "/tmp/fooXXXXXX");  /* terminal Xs will be replaced: */ if (mkdtemp(buf) == NULL) {   perror("mkdtemp failed"); } else {   /* use buf */ } | import "io/ioutil"  // Uses system tmp dir if 1st arg is empty string: path, err := ioutil.TempDir("/tmp", "foo") if err == nil {   fmt.Printf("dir path: %s\n", path) } |
| [system temporary file directory](http://hyperpolyglot.org/c#system-tmp-dir-note) | /* defined in <stdio.h> */ P_tmpdir                          | import "os"  path := os.TempDir()                            |
| [processes and environment](http://hyperpolyglot.org/c#processes-environment-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [command line arguments](http://hyperpolyglot.org/c#cmd-line-arg-note) | int main(int argc, char **argv) {   if (argc > 1)     printf("first arg: %s\n", argv[1]);   return 0; } | import "os"  if len(os.Args) > 1 {   fmt.Printf("first arg: %\n", os.Args[1]) } |
| [program name](http://hyperpolyglot.org/c#program-name-note) | int main(int argc, char **argv) {   printf("program name: %s\n", argv[0]);   return 0; } | import "os"  fmt.Printf("program name: %s\n", os.Args[0])    |
| [environment variable](http://hyperpolyglot.org/c#env-var-note) | #include <stdlib.h>  char *home = getenv("HOME"); setenv("EDITOR", "emacs", 1); unsetenv("EDITOR"); | import "os"  home := os.Getenv("HOME")  err := os.Setenv("EDITOR", "emacs") if err != nil {   fmt.Printf("Setenv failed: %s\n", err) } |
| [iterate over environment variables](http://hyperpolyglot.org/c#env-var-iter-note) | extern char **environ; char **env, *p, *key;  for (env = environ; *env; ++env) {   p = strchr(*env, ’=');   if (p) {     size_t keylen = p - *env;     key = strndup(*env, keylen);     printf("key: %s value: %s\n", key, *env + keylen + 1);     free(key);   } } | import "os" import "strings"  for _, s := range os.Environ() {   a := strings.SplitN(s, "=", 2)   fmt.Printf("key: %s value: %s\n", a[0], a[1]) } |
| [get user id and name](http://hyperpolyglot.org/c#user-id-name-note) | #include <unistd.h>  /* getlogin */  printf("uid: %d\n", getuid()); printf("username: %s\n", getlogin()); | import "os"  os.Getuid() /* username? */                     |
| [exit](http://hyperpolyglot.org/c#exit-note)                 | /* use 0 for success; 1 through 127 for failure */ exit(1);  | import "os"  os.Exit(1)                                      |
| [executable test](http://hyperpolyglot.org/c#executable-test-note) | #include <unistd.h>  if (access("/bin/ls", X_OK) != 0) {   printf("not executable\n"); } |                                                              |
| [external command](http://hyperpolyglot.org/c#external-cmd-note) | /* retval of -1 indicates fork or wait failed.    127 indicates shell failed */ int retval = system("ls -l *"); |                                                              |
| [fork](http://hyperpolyglot.org/c#fork-note)                 |                                                              |                                                              |
| [exec](http://hyperpolyglot.org/c#exec-note)                 |                                                              |                                                              |
| [pipe](http://hyperpolyglot.org/c#pipe-note)                 |                                                              |                                                              |
| [wait](http://hyperpolyglot.org/c#wait-note)                 |                                                              |                                                              |
| [get pid, parent pid](http://hyperpolyglot.org/c#pid-note)   | #include <unistd.h>  /* getpid() and getppid() have return type pid_t */ printf("%d\n", getpid()); printf("%d\n", getppid()) | import "os"  fmt.Println(os.Getpid()) fmt.Println(os.Getppid()) |
| [set signal handler](http://hyperpolyglot.org/c#signal-handler-note) | #include <signal.h>  /* assumes a POSIX environment */ void handle_signal(int signo) {   int restore = errno;   switch(signo) {   case SIGUSR1:     write(1, "caught SIGUSR1\n", 15);     break;   default:     break;   }   errno = restore; }  /* 2nd arg can also be SIG_IGN or SIG_DFL */ sig_t prev_handler = signal(SIGUSR1, &handle_signal);  if (prev_handler == SIG_ERR) {   perror("signal failed");   exit(1); } |                                                              |
| [send signal](http://hyperpolyglot.org/c#send-signal-note)   | #include <signal.h> #include <unistd.h>  /* getppid */  if (kill(getppid(), SIGUSR1) == -1) {   perror("kill failed"); } |                                                              |
| [option parsing](http://hyperpolyglot.org/c#option-parsing-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [getopt](http://hyperpolyglot.org/c#getopt-note)             | #include <getopt.h>  /* 2nd value indicates whether option takes an argument */ static struct option long_opts[] = {   {"debug", no_argument, NULL, 'd'},   {"threshold", required_argument, NULL, 't'},   {0, 0, 0, 0} };  int debug = 0; double threshold = 0.0; char *file = NULL;  int ch; int opti; char *endptr;  while (1) {   ch = getopt_long(argc, argv, "dt:", long_opts, &opti);   if (-1 == ch) {     break;   }    switch (ch) {   case 'd':     debug = 1;     break;   case 't':     threshold = strtod(optarg, &endptr);     if (*endptr != 0) {       fprintf(stderr, "expected float: %s\n", optarg);       exit(1);     }     break;   default:     fprintf(stderr, "unexpected arg: %d\n", ch);     exit(1);   } }  /* optind is index of 1st arg not consumed by getopt */ if (optind != argc - 1) {   fputs("USAGE: foo [--multi] [--threshold=NUM] FILE\n",         stderr);   exit(1); } else {   file = argv[optind]; } | var debug bool var threshold int  flag.BoolVar(&debug, "debug", false, "debug mode") flag.IntVar(&threshold, "threshold", 100, "threshold value") flag.Parse()  // e.g. could call executable with // //    -debug -threshold 200 |
| [libraries and namespaces](http://hyperpolyglot.org/c#libraries-namespaces-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [load library](http://hyperpolyglot.org/c#load-lib-note)     | /* The library must also be linked:       $ gcc foo.o main.c     If the library is in an archive:       $ gcc -lfoo main.c */ #include "foo.h" | import "foo"  // Only capitalized identifiers are visible: var bar = foo.GetBar() |
| [load library in subdirectory](http://hyperpolyglot.org/c#load-lib-subdir-note) | #include "lib/foo.h"                                         | import "lib/foo"                                             |
| [library path](http://hyperpolyglot.org/c#lib-path-note)     | *Add directory to path searched by* #include *directive:* $ gcc -I/home/fred/include foo.c  *Add directory to path searched by -l (lowercase L) option:* $ gcc -L/home/fred/lib -lbar foo.c | *The installation libraries are in the* GOROOT *directory. Additional directories can be listed in the* GOPATH *environment variable. The directories are separated by colons (semicolons) on Unix (Windows).Each directory contains a* src *subdirectory containing source code and potentially a* pkg/ARCH *subdirectory containing compiled libraries.* |
| [declare namespace](http://hyperpolyglot.org/c#declare-namespace-note) | *none*                                                       | // A package declaration must be first statement // in every source file.. package foo |
| [alias namespace](http://hyperpolyglot.org/c#alias-namespace-note) | *none*                                                       | import fu "foo"                                              |
| [unqualified import of namespace](http://hyperpolyglot.org/c#unqualified-import-note) | *none*                                                       | import . "foo"                                               |
| unqualified import of definitions                            |                                                              |                                                              |
| [package manager](http://hyperpolyglot.org/c#pkg-manager-note) *search, install, list installed* |                                                              |                                                              |
| [objects](http://hyperpolyglot.org/c#objects-note)           |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [define class](http://hyperpolyglot.org/c#def-class-note)    |                                                              | // Methods can be defined for any Go type. // Thus a type definition can be regarded as a class definition. type Counter struct {   value int } |
| [create object](http://hyperpolyglot.org/c#create-object-note) |                                                              | cnt := Counter{value: 7}                                     |
| [define method](http://hyperpolyglot.org/c#def-method-note)  |                                                              | func (cnt Counter) Value() int {   return cnt.value }  // receiver must be pointer if method modifies it: func (cnt *Counter) Incr() {   cnt.value++ } |
| [invoke method](http://hyperpolyglot.org/c#invoke-method-note) |                                                              | // same syntax for pointer and non-pointer receiver: cnt.Incr() |
| [subclass](http://hyperpolyglot.org/c#subclass-note)         |                                                              | // An abstract superclass can be declared // using the interface keyword: type Incrementable interface {   Incr()   Value() int }  func IncrAndPrint(incr Incrementable) { )   incr.Incr()   fmt.Printf("incr: %d\n", incr.Value()) }  cnt := Counter{value: 8} IncrAndPrint(&cnt) |
| [user-defined types](http://hyperpolyglot.org/c#user-defined-types-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [typedef](http://hyperpolyglot.org/c#typedef-note)           | typedef int customer_id; customer_id cid = 3;                | type customer_id int  var cid customer_id cid = 3            |
| [enum](http://hyperpolyglot.org/c#enum-note)                 | enum day_of_week {   mon, tue, wed, thu, fri, sat, sun };  enum day_of_week dow = tue; |                                                              |
| [struct definition](http://hyperpolyglot.org/c#struct-definition) | struct medal_count {   const char* country;   int gold;   int silver;   int bronze; }; | type MedalCount struct {   country string   gold int   silver int   bronze int } |
| [struct declaration](http://hyperpolyglot.org/c#struct-declaration) | struct medal_count spain;                                    |                                                              |
| [struct initialization](http://hyperpolyglot.org/c#struct-initialization) | struct medal_count spain = {"Spain", 3, 7, 4};  struct medal_count france = {   .gold = 8,   .silver = 7,   .bronze = 9,   .country = "France" }; | spain := MedalCount{"Spain", 3, 2, 1}  france := MedalCount{   bronze: 9,   silver: 7,   gold: 8,   country: "France"} |
| [struct literal](http://hyperpolyglot.org/c#struct-literal-note) | struct medal_count france;  france = (struct medal_count) {   .gold = 8,   .silver = 7,   .bronze = 9,   .country = "France" }; |                                                              |
| [struct member assignment](http://hyperpolyglot.org/c#struct-member-assignment) | spain.country = "Spain"; spain.gold = 3; spain.silver = 7; spain.bronze = 4; | france := MedalCount{} france.country = "France" france.gold = 7 france.silver = 6 france.bronze = 5 |
| [struct member access](http://hyperpolyglot.org/c#struct-member-access) | int spain_total = spain.gold + spain.silver + spain.bronze;  | france_total = france.gold +   france.silver +   france.bronze |
| [c preprocessor macros](http://hyperpolyglot.org/c#cpp-macros-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [include file](http://hyperpolyglot.org/c#include-file-note) | /* search path include system directories: */ #include <stdio.h>  /* search path also includes directory of source file */ #include "foo.h" |                                                              |
| [add system directory](http://hyperpolyglot.org/c#add-system-dir-note) | $ gcc -I/opt/local/include foo.c                             |                                                              |
| [define macro](http://hyperpolyglot.org/c#def-macro-note)    | #define PI 3.14                                              |                                                              |
| [command line macro](http://hyperpolyglot.org/c#cmd-line-macro-note) | $ gcc -DPI=3.14 foo.c                                        |                                                              |
| [undefine macro](http://hyperpolyglot.org/c#undef-macro-note) | #undef PI                                                    |                                                              |
| macro with arguments                                         | #define MIN(X, Y) ((X) < (Y) ? (X) : (Y))                    |                                                              |
| stringify macro argument                                     |                                                              |                                                              |
| concatenate tokens                                           |                                                              |                                                              |
| conditional compilation                                      | #if defined __WIN32   win32_prinft("%f\n", x); #else   printf("%f\n", x); #endif |                                                              |
| macro operators                                              | *The conditional of* #if *can contain integer literals and the following operators:*  && \|\| ! == != < > <= >= + - * / %  << >> & \| ^ ~   *In addition, the* defined() *operator can be used to test whether a macro is defined.*  #ifdef FOO *is a shortcut for* #if defined(FOO) |                                                              |
| [net and web](http://hyperpolyglot.org/c#net-web-note)       |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [http get](http://hyperpolyglot.org/c#http-get-note)         |                                                              | import "io/ioutil" import "net/http"  resp, err := http.Get("http://www.google.com") if err == nil {   defer resp.Body.Close()   body, err := ioutil.ReadAll(resp.Body)   if err == nil {     fmt.Println(string(body))   } } |
| [unit tests](http://hyperpolyglot.org/c#unit-tests-note)     |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [example](http://hyperpolyglot.org/c#unit-test-example-note) | $ sudo apt-get install check  $ cat > check_foo.c #include <check.h>  START_TEST(test_foo) {   fail_unless(0, "not true"); } END_TEST  Suite * suite_foo(void) {   Suite *ste = suite_create("suite: foo");   TCase *tc = tcase_create("case: foo");    tcase_add_test(tc, test_foo);   suite_add_tcase(ste, tc);    return ste; }  int main(void) {   int number_failed;   Suite *ste = suite_foo();   SRunner *sr = srunner_create(ste);    srunner_run_all(sr, CK_NORMAL);   number_failed = srunner_ntests_failed(sr);   srunner_free(sr);    return (number_failed); }  $ gcc -o check_foo check_foo.c -lcheck  $ ./check_foo Running suite(s): foo 0%: Checks: 1, Failures: 1, Errors: 0 check_foo.c:4:F:foo:test_foo:0: not equal | $ cat foo_test.go package foo  import "testing"  func TestFoo(t *testing.T) {   t.Errorf("always fails") }  $ go test - FAIL: TestFoo (0.00s)   foo_test.go:6: always fails FAIL exit status 1 FAIL _/Users/john/Lang/Go 0.007s |
| [debugging and profiling](http://hyperpolyglot.org/c#debugging-profiling-note) |                                                              |                                                              |
|                                                              | c                                                            | go                                                           |
| [check syntax](http://hyperpolyglot.org/c#check-syntax-note) | $ gcc -fsyntax-only foo.c                                    | $ go vet                                                     |
| [flag for stronger warnings](http://hyperpolyglot.org/c#stronger-warnings-note) | $ gcc -Wall foo.c                                            |                                                              |
| [suppress warnings](http://hyperpolyglot.org/c#suppress-warnings-note) | $ gcc -w foo.c                                               |                                                              |
| [treat warnings as errors](http://hyperpolyglot.org/c#warnings-as-err-note) | $ gcc -Werror foo.c                                          |                                                              |
| [lint](http://hyperpolyglot.org/c#lint-note)                 | $ sudo apt-get install splint $ splint foo.c                 |                                                              |
| [source cleanup](http://hyperpolyglot.org/c#src-cleanup-note) |                                                              | $ go fmt                                                     |
| [run debugger](http://hyperpolyglot.org/c#debugger-note)     | $ gcc -g -o foo foo.c $ gdb foo                              |                                                              |
| [debugger commands](http://hyperpolyglot.org/c#debugger-cmds-note) *help, list source, (re)load executable, next, step, set breakpoint, show breakpoints, delete breakpoint, continue, backtrace, up stack, down stack, print, run, quit* | > h > l [FIRST_LINENO, LAST_LINENO] > file PATH > n > s > b [FILE:]LINENO > i > d NUM > c > bt > up > do > p EXPR > r [ARG1[, [ARG2 ...]] > q |                                                              |
| [benchmark code](http://hyperpolyglot.org/c#benchmark-note)  | #include <sys/times.h> #include <unistd.h>  /* sysconf */  struct tms start, end;  double ticks_per_s = (double)sysconf(_SC_CLK_TCK);  clock_t start_wall = times(&start);  if (start_wall < 0) {   fputs("times failed", stderr);   return (1); }  int i; for (i = 0; i < 1000 * 1000 * 1000; ++i) {   /* empty loop */ }  clock_t end_wall = times(&end);  if (end_wall < 0) {   fputs("times failed", stderr);   return (1); }  clock_t wall = end_wall - start_wall; clock_t user = end.tms_utime - start.tms_utime; clock_t system = end.tms_stime - start.tms_stime;  printf("wall: %f s\n", wall / ticks_per_s); printf("user: %f s\n", user / ticks_per_s); printf("system: %f s\n", system / ticks_per_s); | $ cat foo_test.go package foo  import "testing"  func BenchmarkFoo(b *testing.B) {   for i := 0; i < 1000 * 1000 * 1000; i++ {   } }  $ go test -bench . goos: darwin goarch: amd64 BenchmarkFoo-8  1000000000  0.29 ns/op PASS ok _/Users/john/Lang/go 3.709s |
| [profile code](http://hyperpolyglot.org/c#profile-note)      | *does not work on Mac OS X* $ gcc -pg -o foo foo.c $ ./foo $ gprof foo | $ cat foo_test.go package foo  import "flag" import "fmt" import "testing"  var cpuprofile = flag.String("cpuprofile", "", "")  func Foo() int {   for j := 0; j < 100; j++ {   }   return 1 }  func BenchmarkFoo(b *testing.B) {   for i := 0; i < 1000 * 1000 * 10; i++ {     j := Foo()     if j > 10 {       fmt.Printf("Unexpected")     }   } }  $ go tool pprof cpu.prof *type "top" to see profile* |
| [memory tool](http://hyperpolyglot.org/c#memory-tool-note)   | $ sudo apt-get install valgrind $ gcc -o foo foo.c $ valgrind foo |                                                              |
|                                                              | _________________________________________________________________ | _________________________________________________________________ |



## [Version](http://hyperpolyglot.org/c#version)



## [version used](http://hyperpolyglot.org/c#version-used)

The compiler version used for this cheatsheat.



## [show version](http://hyperpolyglot.org/c#show-version)

How to get the compiler version.



## [implicit prologue](http://hyperpolyglot.org/c#implicit-prologue)

Code which the examples in this sheet assume to have been executed.

**c:**

A selection of commonly used symbols and macros from the standard C library and the headers in which they are defined according to POSIX:

| [errno.h](http://pubs.opengroup.org/onlinepubs/9699919799/functions/errno.html) | [stdlib.h](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/stdlib.h.html) | [stdio.h](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/stdio.h.html) | [string.h](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/string.h.html) | [time.h](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/time.h.html) | [wchar.h](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/wchar.h.html) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| errno  ENOENT ENOMEM EACCES EINVAL EPIPE                     | abs drand48 exit free getenv lrand48 malloc mkdtemp putenv qsort realpath srand strtod strtol system unsetenv | fclose feof fflush fgets fopen fprintf fputs getc getline printf putc remove rename scanf  BUFSIZ EOF NULL | strcat strchr strcmp strcpy strdup strerror strncat strncmp strncpy strndup strrchr strstr strtok | time time_t                                                  | swprintf wcscmp wcsdup wcslen wprintf                        |



# [Grammar and Invocation](http://hyperpolyglot.org/c#grammar-invocation)



## [hello world](http://hyperpolyglot.org/c#hello-world)

How to write, compile, and run a "Hello, World!" program.



## [file suffixes](http://hyperpolyglot.org/c#file-suffixes)

The suffixes used for source files, header files, and compiled object files.



## [statement separator](http://hyperpolyglot.org/c#stmt-separator)

How statements are terminated.



## [block delimiters](http://hyperpolyglot.org/c#block-delimiters)

How a block of statements is delimited.



## [end-of-line comment](http://hyperpolyglot.org/c#eol-comment)

The syntax for a comment which is terminated by the end of the line.

**c:**

The `//` style comment first appeared in the C99 standard.



## [multiple line comment](http://hyperpolyglot.org/c#multiple-line-comment)

The syntax for a comment which can span multiple lines.

`/* */` style comments cannot be nested in C or Go.



# [Variables and Expressions](http://hyperpolyglot.org/c#variables-expressions)



## [variable](http://hyperpolyglot.org/c#local-var)

How to declare a variable.



## [free heap](http://hyperpolyglot.org/c#free-heap)

How to free memory allocated on the heap.



## [global variable](http://hyperpolyglot.org/c#global-var)

How to declare a global variable.



## [uninitialized variable](http://hyperpolyglot.org/c#uninitialized-var)

What happens when reading from an uninitialized variable.



## [compile time constant](http://hyperpolyglot.org/c#compile-time-const)

How to define a constant.

**go:**

Multiple constants can be declared in this manner:

```
const (
  Pi = 3.14
  E = 2.718
)
```



## [immutable variable](http://hyperpolyglot.org/c#immutable-var)

How to declare a variable which cannot change after initialization.



## [assignment](http://hyperpolyglot.org/c#assignment)

The syntax for assigning a value to a variable.



## [parallel assignment](http://hyperpolyglot.org/c#parallel-assignment)

The syntax for parallel assignment.



## [swap](http://hyperpolyglot.org/c#swap)

How to swap the values in two variables.



## [compound assignment](http://hyperpolyglot.org/c#compound-assignment)

The compound assignment operators.



## [increment and decrement](http://hyperpolyglot.org/c#incr-decr)

The increment and decrement operators.



## [null](http://hyperpolyglot.org/c#null)

The null literal and where the null value can be used.

**c:**

A typical definition:

```
#define NULL (void *)0
```



## [null test](http://hyperpolyglot.org/c#null-test)

How to test whether a value is null.



## [conditional expression](http://hyperpolyglot.org/c#conditional-expr)

The syntax for a conditional expression.



# [Arithmetic and Logic](http://hyperpolyglot.org/c#arithmetic-logic)



## [boolean type](http://hyperpolyglot.org/c#boolean-type)

**c:**

The following definitions are common:

```
typedef int BOOL;
#define TRUE 1
#define FALSE 0
```



## [true and false](http://hyperpolyglot.org/c#true-false)

Literals for the boolean values true and false.

**c:**

The following definitions are common:

```
typedef int BOOL;
#define TRUE 1
#define FALSE 0
```



## [falsehoods](http://hyperpolyglot.org/c#falsehoods)

Values which evaluate as false in the conditional expression of an `if` statement.



## [logical operators](http://hyperpolyglot.org/c#logical-op)

The logical operators.

In all languages on this sheet the && and || operators short circuit: i.e. && will not evaluate the 2nd argument if the 1st argument is false, and || will not evaluate the 2nd argument if the 1st argument is true. If the 2nd argument is not evaluated, side-effects that it contains are not executed.



## [relational operators](http://hyperpolyglot.org/c#relational-op)

Binary operators which return boolean values.



## [integer type](http://hyperpolyglot.org/c#int-type)

Signed integer types.

**c:**

Whether *char* is a signed or unsigned type depends on the implementation.



## [unsigned type](http://hyperpolyglot.org/c#unsigned-type)

Unsigned integer types.

**c:**

Whether *char* is a signed or unsigned type depends on the implmentation.



## [float type](http://hyperpolyglot.org/c#float-type)

Floating point types.



## [arithmetic operators](http://hyperpolyglot.org/c#arith-op)

The arithmetic binary operators.



## [integer division](http://hyperpolyglot.org/c#int-div)

How to find the quotient of two integers.



## [integer division by zero](http://hyperpolyglot.org/c#int-div-zero)

The result of attempting to divide an integer by zero.

**c:**

The behavior for division by zero is system dependent; the behavior described is common on Unix.



## [float division](http://hyperpolyglot.org/c#float-div)

How to perform float division on integers.



## [float division by zero](http://hyperpolyglot.org/c#float-div-zero)

The result of attempting to divide a float by zero.



## [power](http://hyperpolyglot.org/c#power)

How to perform exponentiation.



## [sqrt](http://hyperpolyglot.org/c#sqrt)

The square root function.



## [sqrt -1](http://hyperpolyglot.org/c#sqrt-negative-one)

The result of attempting to find the square root of a negative nubmer.



## [transcendental functions](http://hyperpolyglot.org/c#transcendental-func)

The exponential function; logarithm functions; trigonometric and inverse trigonometric functions.



## [transcendental constants](http://hyperpolyglot.org/c#transcendental-const)

Constants for `π` and `e`.



## [float truncation](http://hyperpolyglot.org/c#float-truncation)

Functions for converting a float to a nearby integer value.

**c:**

The `math.h` library also provides `floor` and `ceil` which return `double` values.



## [absolute value](http://hyperpolyglot.org/c#absolute-val)

The absolute value of a numeric.



## [complex type](http://hyperpolyglot.org/c#complex-type)

Complex floating point types.



## [complex construction](http://hyperpolyglot.org/c#complex-construction)

How to create a complex number.

**c:**

The C11 standard introduced macros for constructing complex numbers which work correctly when the arguments are inf, nan, or +nan:

```
     double complex CMPLX(double x, double y)
     float complex CMPLXF(float x, float y)
     long double complex CMPLXL(long double x, long double y)
```



## [complex decomposition](http://hyperpolyglot.org/c#complex-decomposition)

How to decompose a complex number into its real and imaginary parts; how to get the argument and absolute value of a complex number; how to get its complex conjugate.



## [random number](http://hyperpolyglot.org/c#random-num)

How to generate a random integer from a uniform distribution; how to generate a random float from a uniform distribution.



## [random seed](http://hyperpolyglot.org/c#random-seed)

How to set the random seed.

**c:**

There are at least three random number generators defined in `stdlib.h`. Each has its own function for setting the random seed:

```
srand(17);    /* used by rand() */

srandom(17);  /* used by random() */

srand48(17);  /* used by drand48() and lrand48() */
```



## [bit operators](http://hyperpolyglot.org/c#bit-op)

The bit operations: right shift, left shift, and, or, exclusive or, and not.

**go:**

Note that ^ is bit-not and not exclusive-or like in C.



## [binary, octal, and hex literals](http://hyperpolyglot.org/c#binary-octal-hex)



# [Strings](http://hyperpolyglot.org/c#strings)



## [string type](http://hyperpolyglot.org/c#str-type)

The type for a string.

**c:**

The C11 standard introduces `char16_t` and `char32_t`, but no literal syntax or functions which take them as arguments.



## [string literal](http://hyperpolyglot.org/c#str-literal)

The syntax for a string literal.

**go:**

The backquote literal is also called the raw string literal. It has no escape sequences; it cannot contain a backquote character.



## [newline in string literal](http://hyperpolyglot.org/c#newline-in-str-literal)

Can newlines be included in string literals?

**c:**

The compiler will convert the following three string literals to the single literal `"foobarbaz"`.

```
char *metavars = "foo"
  "bar"
  "baz";
```



## [string escapes](http://hyperpolyglot.org/c#str-literal-esc)

Escape sequences in string literals.



## [compare strings](http://hyperpolyglot.org/c#compare-str)

**c:**

Returns 1, 0, or -1 depending upon whether the first string is lexicographically greater, equal, or less than the second. The variants *strncmp*, *strcasecmp*, and *strncasecmp* can perform comparisons on the first *n* characters of the strings or case insensitive comparisons.



## [string to number](http://hyperpolyglot.org/c#str-to-num)

**c:**

*strtoimax*, *strtol*, *strtoll*, *strtoumax*, *strtoul*, and *strtoull* take three arguments:

```
intmax_t
strtoimax(const char *str, char **endp, int base);
```

The 2nd argument, if not NULL, will be set to first character in the string that is not part of the number. The 3rd argument can specify a base between 2 and 36.

*strtof*, *strtod*, and *strtold* take three arguments:

```
double
strtod(const char *str, char **endp);
```



## [number to string](http://hyperpolyglot.org/c#num-to-str)



## [split](http://hyperpolyglot.org/c#split)



## [join](http://hyperpolyglot.org/c#str-join)



## [concatenate](http://hyperpolyglot.org/c#str-concat)



## [replicate](http://hyperpolyglot.org/c#str-replicate)



## [extract substring](http://hyperpolyglot.org/c#extract-substr)



## [index of substring](http://hyperpolyglot.org/c#index-substr)



## [format string](http://hyperpolyglot.org/c#fmt-str)



## [translate case](http://hyperpolyglot.org/c#translate-case)



## [trim](http://hyperpolyglot.org/c#trim)



## [pad](http://hyperpolyglot.org/c#pad)



## [length](http://hyperpolyglot.org/c#str-len)



## [character type](http://hyperpolyglot.org/c#char-type)

The type for a character.



## [character literal](http://hyperpolyglot.org/c#char-literal)



## [character lookup](http://hyperpolyglot.org/c#char-lookup)



## [character index](http://hyperpolyglot.org/c#char-index)



## [character tests](http://hyperpolyglot.org/c#char-tests)



## [chr and ord](http://hyperpolyglot.org/c#chr-ord)



# [Regular Expressions](http://hyperpolyglot.org/c#regexes)



## [metacharacters](http://hyperpolyglot.org/c#regex-metachar)

The list of regular expression metacharacters.

A regular expression that does not contain any metacharacters matches itself as a string.



## [character class abbrevations](http://hyperpolyglot.org/c#char-class-abbrev)

Abbreviations for character classes.

**c:**

[regex.h (POSIX 2008)](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/regex.h.html#tag_13_38)

We describe the `regex` library which is mandated by POSIX.

The PCRE library is available or easily installed on most systems and provides Perl style regular expressions. In particular PCRE has these character class abbreviations: `\d \D \h \H \s \S \v \V \w \W`.

To install PCRE on Ubuntu and read the documentation:

```
$ sudo apt-get install pcre

$ man pcre
```

To include the PCRE definitions in a C file:

```
#include <pcre.h>
```



## [anchors](http://hyperpolyglot.org/c#regex-anchors)

Metacharacters for matching locations in the string which aren't single characters or substrings.



## [match test](http://hyperpolyglot.org/c#regex-test)

How to test whether a string matches a regular expression.



## [case insensitive match test](http://hyperpolyglot.org/c#case-insensitive-regex)

How to test whether a string matches a regular expression in a case insensitive manner.



## [modifers](http://hyperpolyglot.org/c#regex-modifiers)

Modifers which can be used to customize the behvaior of a regular expression.

**go:**

The meaning of the modifiers:

| i    | case insensitive match                                       |
| ---- | ------------------------------------------------------------ |
| m    | ^ and $ match begin and end of line in addition to begin and end of string |
| s    | l. matches \n                                                |
| U    | make (foo)*, (foo)+ non-greedy and (foo)*?, (foo)+? greedy   |



## [substitution](http://hyperpolyglot.org/c#subst)

How to replace the part of a string matching a regular expression.



## [group capture](http://hyperpolyglot.org/c#group-capture)

How to use a regular expression to parse a string.



# [Dates and Time](http://hyperpolyglot.org/c#dates-time)



## [unix epoch type](http://hyperpolyglot.org/c#unix-epoch-type)



## [broken-down datetime type](http://hyperpolyglot.org/c#broken-down-datetime-type)



## [current unix epoch](http://hyperpolyglot.org/c#current-unix-epoch)



## [current datetime](http://hyperpolyglot.org/c#current-datetime)



## [broken-down datetime to unix epoch](http://hyperpolyglot.org/c#broken-down-datetime-to-unix-epoch)



## [unix epoch to broken-down datetime](http://hyperpolyglot.org/c#unix-epoch-to-broken-down-datetime)



## [format datetime](http://hyperpolyglot.org/c#fmt-datetime)



## [parse datetime](http://hyperpolyglot.org/c#parse-datetime)



## [date subtraction](http://hyperpolyglot.org/c#date-subtraction)



## [add duration](http://hyperpolyglot.org/c#add-duration)



## [date parts](http://hyperpolyglot.org/c#date-parts)



## [time parts](http://hyperpolyglot.org/c#time-parts)



## [build broken-down datetime](http://hyperpolyglot.org/c#build-datetime)



## [local time zone determination](http://hyperpolyglot.org/c#local-tmz-determination)



## [time zone info](http://hyperpolyglot.org/c#tmz-info)



## [daylight savings test](http://hyperpolyglot.org/c#daylight-savings-test)



## [microseconds](http://hyperpolyglot.org/c#microseconds)



# [Fixed-Length Arrays](http://hyperpolyglot.org/c#fixed-length-arrays)



## [declare](http://hyperpolyglot.org/c#declare-array)

How to declare an array variable.



## [allocate on stack](http://hyperpolyglot.org/c#allocate-array-on-stack)

How to allocate an array on the stack.



## [allocate on heap](http://hyperpolyglot.org/c#allocate-array-on-heap)

How to allocate an array on the heap.



## [free heap](http://hyperpolyglot.org/c#free-array-on-heap)

How to free an array that was allocated on the heap.



## [literal](http://hyperpolyglot.org/c#array-literal)

Syntax for an array literal.



## [size](http://hyperpolyglot.org/c#array-size)

How many elements are stored in an array.



## [lookup](http://hyperpolyglot.org/c#array-lookup)

How to get an element by index.

**c:**

Arrays can be manipulated with pointer syntax. The following sets *x* and *y* to the same value:

```
int a[] = {3,7,4,8,5,9,6,10};
int x = a[4];
int y = *(a+4);
```



## [update](http://hyperpolyglot.org/c#array-update)

How to set or change the element stored at an index.



## [out-of-bounds behavior](http://hyperpolyglot.org/c#array-out-of-bounds)

What happens when an attempt is made to access an element at an invalid index.



## [element index](http://hyperpolyglot.org/c#array-element-index)



## [slice](http://hyperpolyglot.org/c#slice-array)



## [slice to end](http://hyperpolyglot.org/c#slice-array-to-end)



## [manipulate back](http://hyperpolyglot.org/c#array-back)



## [manipulate front](http://hyperpolyglot.org/c#array-front)



## [concatenate](http://hyperpolyglot.org/c#concatenate-array)



## [copy](http://hyperpolyglot.org/c#copy-array)



## [iterate over elements](http://hyperpolyglot.org/c#iterate-over-array)

How to iterate over the elements of an array.

**c:**

C arrays do not store their size; if needed the information can be stored in a separate variable. Another option is to use a special value to mark the end of the array:

```
char *a[] = { "Bob", "Ned", "Amy", NULL };
int i;
for (i=0; a[i]; i++) {
  printf("%s\n", a[i]);
}
```



## [reverse](http://hyperpolyglot.org/c#reverse-array)

How to reverse the elements of an array.



## [sort](http://hyperpolyglot.org/c#sort-array)

How to sort the elements of an array.



# [Resizable Arrays](http://hyperpolyglot.org/c#resizable-arrays)



## [declare](http://hyperpolyglot.org/c#declare-resizable-array)

How to declare a resizable array variable.



## [literal](http://hyperpolyglot.org/c#resizable-array-literal)

Syntax for a resizable array literal.



## [size](http://hyperpolyglot.org/c#resizable-array-size)

How many elements are stored in a resizable array.



## [lookup](http://hyperpolyglot.org/c#resizable-array-lookup)

How to get an element by index.

**c:**

Arrays can be manipulated with pointer syntax. The following sets *x* and *y* to the same value:

```
int a[] = {3,7,4,8,5,9,6,10};
int x = a[4];
int y = *(a+4);
```



## [update](http://hyperpolyglot.org/c#resizable-array-update)

How to set or change the element stored at an index.



## [resizable to fixed array](http://hyperpolyglot.org/c#resizable-to-fixed)

How to convert a resizable array to a fixed array.



## [fixed to resizable array](http://hyperpolyglot.org/c#fixed-to-resizable)

How to convert a fixed array to a resizable array.



## [out-of-bounds behavior](http://hyperpolyglot.org/c#resizable-array-out-of-bounds)

What happens when an attempt is made to access an element at an invalid index.



## [element index](http://hyperpolyglot.org/c#resizable-array-element-index)

How to get the index of an element in a resizable array.



## [slice](http://hyperpolyglot.org/c#slice-resizable-array)

How to slice a resizable array.



## [slice to end](http://hyperpolyglot.org/c#slice-resizable-array-to-end)

How to slice a resizable array to the end.



## [manipulate back](http://hyperpolyglot.org/c#resizable-array-back)

How to add and remove elements from the back of a resizable array.



## [manipulate front](http://hyperpolyglot.org/c#resizable-array-front)

How to add and remove elements from the front of a resizable array.



## [concatenate](http://hyperpolyglot.org/c#concatenate-resizable-array)

How to concatenate resizable arrays.



## [copy](http://hyperpolyglot.org/c#copy-resizable-array)

How to copy a resizable array.



## [iterate over elements](http://hyperpolyglot.org/c#iterate-over-resizable-array)

How to iterate over the elements of a resizable array.

**c:**

C arrays do not store their size; if needed the information can be stored in a separate variable. Another option is to use a special value to mark the end of the array:

```
char *a[] = { "Bob", "Ned", "Amy", NULL };
int i;
for (i=0; a[i]; i++) {
  printf("%s\n", a[i]);
}
```



## [iterate over indices and elements](http://hyperpolyglot.org/c#iterate-indices-elem)

How to iterate over the indices and elements of a resizable array.



## [reverse](http://hyperpolyglot.org/c#reverse-resizable-array)

How to reverse the elements of a resizable array.



## [sort](http://hyperpolyglot.org/c#sort-resizable-array)

How to sort the elements of a resizable array.



# [Dictionaries](http://hyperpolyglot.org/c#dictionaries)



## [declare](http://hyperpolyglot.org/c#declare-dict)



## [literal](http://hyperpolyglot.org/c#dict-literal)



## [size](http://hyperpolyglot.org/c#dict-size)



## [lookup](http://hyperpolyglot.org/c#dict-lookup)



## [update](http://hyperpolyglot.org/c#dict-update)



## [missing key behavior](http://hyperpolyglot.org/c#dict-missing-key)



## [is key present](http://hyperpolyglot.org/c#dict-is-key-present)



## [delete](http://hyperpolyglot.org/c#dict-delete)



## [iterate](http://hyperpolyglot.org/c#dict-iter)



# [Functions](http://hyperpolyglot.org/c#functions)



## [define function](http://hyperpolyglot.org/c#def-func)

How to define a function.



## [invoke function](http://hyperpolyglot.org/c#invoke-func)

How to invoke a function.



## [forward declaration of function](http://hyperpolyglot.org/c#forward-decl-func)

How to declare a function without defining it.



## [overload function](http://hyperpolyglot.org/c#overload-func)

How to define multiple functions with the same name. The functions differ in either the number or type of arguments.



## [nest function](http://hyperpolyglot.org/c#nest-func)

How to define a function inside another function.



## [default value for parameter](http://hyperpolyglot.org/c#default-val-param)



## [variable number of arguments](http://hyperpolyglot.org/c#variable-num-arg)

**c:**

The stdarg.h library supports variable length functions, but provides no means for the callee to determine how many arguments were provided. Two techniques for communicating the number of arguments to the caller are (1) devote one of the non-variable arguments for the purpose as illustrated in the table above, or (2) set the last argument to a sentinel value as illustrated below. Both techniques permit the caller to make a mistake that can cause the program to segfault. *printf* uses the first technique, because it infers the number of arguments from the number of format specifiers in the format string.

```
char* concat(char* first,  ...) {

  int len;
  va_list ap;
  char *retval, *arg;

  va_start(ap, first);
  len = strlen(first);

  while (1) {
    arg = va_arg(ap, char*);
    if (!arg) {
      break;
    }
    len += strlen(arg);
  }

  va_end(ap);

  retval = calloc(len+1, sizeof *retval);

  va_start(ap, first);

  strcpy(retval, first);
  len = strlen(first);

  while (1) {
    arg = va_arg(ap, char*);
    if (!arg) {
      break;
    }
    printf("copying %s\n", arg);
    strcpy(retval+len, arg);
    len += strlen(arg);
  }

  va_end(ap);

  return retval;
}
```

An example of use:

```
string *s = concat("Hello", ", ", "World", "!", NULL);
```



## [named parameters](http://hyperpolyglot.org/c#named-param)



## [pass by value](http://hyperpolyglot.org/c#pass-by-val)



## [pass by address](http://hyperpolyglot.org/c#pass-by-addr)



## [return value](http://hyperpolyglot.org/c#retval)

How the return value for a function is determined.



## [no return value](http://hyperpolyglot.org/c#no-retval)

How to define a function with no return value.

**swift:**

The return value can be explicitly declared as `Void`:

```
func print_err(err: String) -> Void {
  println(err)
}
```



## [multiple return values](http://hyperpolyglot.org/c#multiple-retval)

How to return multiple values.



## [named return values](http://hyperpolyglot.org/c#named-retval)

How to return values by assigning values to variables.



## [execute on return](http://hyperpolyglot.org/c#exec-on-return)

How to register a function to be executed on return of the calling function.

**go:**

Arguments of the on-return function are evaluated at the time the function is registered and not when the caller returns.

Multiple on-return functions are evaluated in LIFO order.



## [anonymous function literal](http://hyperpolyglot.org/c#anonymous-func-literal)



## [invoke anonymous function](http://hyperpolyglot.org/c#invoke-anonymous-func)



## [function with private state](http://hyperpolyglot.org/c#func-private-state)



## [closure](http://hyperpolyglot.org/c#closure)



## [function as value](http://hyperpolyglot.org/c#func-as-val)



# [Execution Control](http://hyperpolyglot.org/c#execution-control)



## [if](http://hyperpolyglot.org/c#if)

The if statement.

An if statement is a series of blocks, each guarded by a conditional expression. The first conditional expression statement which evaluates to true determines the block which executes. An optional else block executes if none of the of the conditional expressions are true.



## [switch](http://hyperpolyglot.org/c#switch)

The switch statement.

The switch statement has a switch expression which is evaluated against one or more case values. The first case value which is equal to the switch expression determines the block which executes. An optional default block executes if none of the case values are equal.

Note that in some languages, execution "falls through" to the next block in a switch unless prevented by a break statement.

**go:**

Case values can be expressions.

The switch statement can lack a switch expression, in which case the first case value which evaluates to true determines the block to execute. Such a switch statement differs little from an if statement, but note that `fallthrough` cannot be used in an if statement.

It is possible to switch on type of an expression, in which case the case values are types:

```
switch x.(type) {
case nil:
  printString("x is nil")
case int:
  printString("x is int")
case float64:
  printFloat64("x is float64")
default:
  printString("unknown type")
}
```



## [while](http://hyperpolyglot.org/c#while)

A while loop is a conditional expression and a block. The conditional expression is evaluated before each execution of the block. The block is executed iteratively as long as the conditional expression is true.

**c:**

C has a do-while statement. The block is always executed at least once. The conditional expression is evaluated before the second and subsequent iterations to determine if the block is executed again.

```
int i = 0;

do {
  print("%d\n", ++i);
} while (i < 10);
```

If the body of a while loop consists of a single statement the curly braces are optional:

```
int i = 0;
while (i<10)
  printf("%d\n", ++i);
```



## [for](http://hyperpolyglot.org/c#for)

A for loop has four parts: the *initialization* which executes at the outset, the *condition* which is evaluated before each iteration, the *body* which is executed if the condition is true, and the *afterthought* which is executed after each execution of the body.



## [for with local scope](http://hyperpolyglot.org/c#for-local-scope)

Whether variables declared in the initialization are local to the body.



## [infinite loop](http://hyperpolyglot.org/c#infinite-loop)

The syntax for an infinite loop.



## [break](http://hyperpolyglot.org/c#break)

A break statement is used to exit a loop.



## [break from nested loops](http://hyperpolyglot.org/c#break-from-nested-loops)

How to break out of nested loops.



## [continue](http://hyperpolyglot.org/c#continue)

A continue statement is used to terminate the current iteration of a loop.



## [single statement branches and loops](http://hyperpolyglot.org/c#single-stmt-branch-loop)



## [dangling else](http://hyperpolyglot.org/c#dangling-else)



## [goto](http://hyperpolyglot.org/c#goto)



## [longjmp](http://hyperpolyglot.org/c#longjmp)



# [Concurrency](http://hyperpolyglot.org/c#concurrency)



# [File Handles](http://hyperpolyglot.org/c#file-handles)



## [standard file handles](http://hyperpolyglot.org/c#std-file-handles)

The file handles for standard input, standard output, and standard error.

**c:**

POSIX systems provide processes with the ability to open multiple files and manipulate them with via integers called file descriptors. Normally the integers 0, 1, and 2 refer to standard input, standard output, and standard error. The header <unistd.h> defines the macros STDIN_FILENO, STDOUT_FILENO, and STDERR_FILENO for these file descriptors.

System calls take file descriptors as arguments, but the C standard library provides an alternate set functions for buffered I/O. The standard library functions use `FILE` structs to identify streams and open files.



## [read line from stdin](http://hyperpolyglot.org/c#read-line-stdin)

How to read a line from standard input.



## [write line to stdout](http://hyperpolyglot.org/c#write-line-stdout)

How to write a line to standard output.



## [write formatted string to stdout](http://hyperpolyglot.org/c#printf)

How to print a formatted string to standard out.

**c:**

The [printf man page](http://linux.die.net/man/3/printf) describes the notation used in C style format strings.



## [open file for reading](http://hyperpolyglot.org/c#open-file)

How to open a file for reading.



## [open file for writing](http://hyperpolyglot.org/c#open-file-write)

How to open a file for reading.



## [open file for appending](http://hyperpolyglot.org/c#open-file-append)

How to open a file for appending.



## [close file](http://hyperpolyglot.org/c#close-file)

How to close a file handle.



## [close file implicitly](http://hyperpolyglot.org/c#close-file-implicitly)



## [i/o errors](http://hyperpolyglot.org/c#io-err)



## [read line](http://hyperpolyglot.org/c#read-line)



## [iterate over file by line](http://hyperpolyglot.org/c#file-line-iterate)



## [read file into array of strings](http://hyperpolyglot.org/c#read-file-array)



## [read file into string](http://hyperpolyglot.org/c#read-file-str)



## [write string](http://hyperpolyglot.org/c#write-str)



## [write line](http://hyperpolyglot.org/c#write-line)



## [flush file handle](http://hyperpolyglot.org/c#flush)



## [end-of-file test](http://hyperpolyglot.org/c#eof-test)



## [get and set file handle position](http://hyperpolyglot.org/c#seek)



## [open unused file](http://hyperpolyglot.org/c#tmp-file)

How to open a file with a previously unused file name.

**c:**

The function `mkstemps` can be used to create a new file with a fixed suffix: "/tmp/fooXXXXXXsuffix".



# [Files](http://hyperpolyglot.org/c#files)



## [file test, regular file test](http://hyperpolyglot.org/c#file-test)

Does the file exist; is the file a regular file.



## [file size](http://hyperpolyglot.org/c#file-size)

The size of the file in bytes.



## [is file readable, writable, executable](http://hyperpolyglot.org/c#readable-writable-executable)

Can the process read, write, or executable the file?

**c:**

`access` returns 0 if the process has the permission, and -1 if it doesn't or some other error occurred.

`access` uses the real user id to determine permission even though the kernel uses the effective user id.



## [set file permissions](http://hyperpolyglot.org/c#chmod)



## [copy file, remove file, rename file](http://hyperpolyglot.org/c#file-cp-rm-mv)



## [create symlink, symlink test, readlink](http://hyperpolyglot.org/c#symlink)



## [generate unused file name](http://hyperpolyglot.org/c#unused-file-name)



# [File Formats](http://hyperpolyglot.org/c#file-fmt)



# [Directories](http://hyperpolyglot.org/c#directories)



## [working directory](http://hyperpolyglot.org/c#working-dir)



## [build pathname](http://hyperpolyglot.org/c#build-pathname)



## [dirname and basename](http://hyperpolyglot.org/c#dirname-basename)



## [absolute pathname](http://hyperpolyglot.org/c#absolute-pathname)



## [iterate over directory by file](http://hyperpolyglot.org/c#dir-iterate)



## [glob paths](http://hyperpolyglot.org/c#glob)



## [make directory](http://hyperpolyglot.org/c#mkdir)



## [recursive copy](http://hyperpolyglot.org/c#recursive-cp)



## [remove empty directory](http://hyperpolyglot.org/c#rmdir)



## [remove directory and contents](http://hyperpolyglot.org/c#rm-rf)



## [directory test](http://hyperpolyglot.org/c#dir-test)



## [generate unused directory](http://hyperpolyglot.org/c#unused-dir)



## [system temporary file directory](http://hyperpolyglot.org/c#system-tmp-dir)



# [Processes and Environment](http://hyperpolyglot.org/c#processes-environment)



## first argument

**c:**

The first argument is the pathname to the executable. Whether the pathname is absolute or relative depends on how the executable was invoked. If the executable was invoked via a symlink, then the first argument is the pathname of the symlink, not the executable the symlink points to.



## [environment variable](http://hyperpolyglot.org/c#env-var)



## [iterate over environment variables](http://hyperpolyglot.org/c#env-var-iter)



## [exit](http://hyperpolyglot.org/c#exit)

How to set the exit status and cause the process to exit.

**c:**

On POSIX systems zero indicates success and other values indicate failure.

On Linux and Mac OS X the value returned to the parent is `exit_arg & 0377`. If the process exited because of a signal, the kernel sets the exit status to 128 plus the signal number. The signals are numbered starting from 1, leaving exit status values from 1 to 127 and perhaps 128 available for other failure conditions.

The C standard library defines the values EXIT_SUCCESS and EXIT_FAILURE as an aid for writing code which is portable to systems which do not use 0 to indicate success.



## [set signal handler](http://hyperpolyglot.org/c#signal-handler)

How to set a signal handler on a POSIX system.

A quirk about `signal` is that some systems (e.g. Solaris) do not leave the signal handler registered after handling a signal. Mac OS X and Linux do leave the signal handler registered.

For portability, one can used `sigaction` instead of `signal`.

Before writing a signal handler, review the list of permitted functions that you can call from the signal handler. The list is available in `man 2 sigaction` on Mac OS X and `man 7 signal` on Linux.

```
$ man 2 sigaction

$ man 7 signal
```

- re-entrant functions
- sigaction



## [send signal](http://hyperpolyglot.org/c#send-signal)



# [Option Parsing](http://hyperpolyglot.org/c#option-parsing)



# [Libraries and Namespaces](http://hyperpolyglot.org/c#libraries-namespaces)



## [load library](http://hyperpolyglot.org/c#load-lib)

How to load a library.

**c:**

Loading a library is a two part process.

Library declarations are made available by including headers in the client code.

Linking is performed by listing the library objects with the client object containing the `main` function on the command line when invoked the linker.

Alternatively, library objects can be collected into archive files using the `ar` command. These files have a `.a` suffix. The -l (lowercase L) option is used to include an archive when linking.

**go:**

Multiple libraries can be loaded by listing them one after another:

```
import  "fmt"
import "math/rand"
```

Alternatively a single import statement can be used:

```
import (
    "fmt"
    "math/rand"
)
```



## [load library in subdirectory](http://hyperpolyglot.org/c#load-lib-subdir)

How to load a library in a subdirectory of the load path.



## [library path](http://hyperpolyglot.org/c#lib-path)

How to the library path is specified.



## [declare namespace](http://hyperpolyglot.org/c#declare-namespace)

How to declare the namespace of a source file.



## [alias namespace](http://hyperpolyglot.org/c#alias-namespace)

How to import a namespace under an alias.

This can be used to provide an abbreviated name for a namespace.

It also allows a client to use two different libraries which declare the same namespace.



## [unqualified import of namespace](http://hyperpolyglot.org/c#unqualified-import)

How to import all the identifiers in a library so that the client can refer to them without the namespace prefix.



# [Objects](http://hyperpolyglot.org/c#objects)



## [define class](http://hyperpolyglot.org/c#def-class)



## [create object](http://hyperpolyglot.org/c#create-object)



## [define method](http://hyperpolyglot.org/c#def-method)



## [invoke method](http://hyperpolyglot.org/c#invoke-method)



## [subclass](http://hyperpolyglot.org/c#subclass)



# [User-Defined Types](http://hyperpolyglot.org/c#user-defined-types)



## [typedef](http://hyperpolyglot.org/c#typedef)

**c:**

Because C integer types don't have well defined sizes, *typedef* is sometimes employed to as an aid to writing portable code. One might include the following in a header file:

```
typedef int int32_t;
```

The rest of the code would declare integers that need to be 32 bits in size using *int32_t* and if the code needed to be ported to a platform with a 16 bit *int*, only a single place in the code requires change. In practice the *typedef* abstraction is leaky because functions in the standard library such as *atoi*, *strtol*, or the format strings used by *printf* depend on the underlying type used.



## [enum](http://hyperpolyglot.org/c#enum)

**c:**

Enums were added to the C standard when the language was standardized by ANSI in 1989.

An enum defines a family of integer constants. If an integer value is not explicitly provided for a constant, it is given a value one greater than the previous constant in the list. If the first constant in the list is not given an explicit value, it is assigned a value of zero. it is possible for constants in a list to share values. For example, in the following enum, *a* and *c*are both zero and *b* and *d* are both one.

```
enum { a=0, b, c=0, d };
```

A *typedef* can be used to make the *enum* keyword unnecessary in variable declarations:

```
typedef enum { mon, tue, wed, thu, fri, sat, sun } day_of_week;
day_of_week d = tue;
```

From the point of view of the C compiler, an enum is an *int*. The C compiler does not prevent assigning values to an enum type that are not in the enumerated list. Thus, the following code compiles:

```
enum day_of_week { mon, tue, wed, thu, fri, sat, sun };
day_of_week d = 10;

typedef enum { mon, tue, wed, thu, fri, sat, sun } day_of_week2;
day_of_week2 d2 = 10;
```



## struct definition

A struct provides names for elements in a predefined set of data and permits the data to be accessed directly without the intermediation of getters and setters. C++, Java, and C# classes can be used to define structs by making the data members public. However, public data members violates the [uniform access principle](http://en.wikipedia.org/wiki/Uniform_access_principle).



## struct declaration



## struct initialization

**c:**

The literal format for a struct can only be used during initialization. If the member names are not provided, the values must occur in the order used in the definition.



## struct member assignment



## struct member access

**c:**

The period operator used for member access has higher precedence than the pointer operator. Thus parens must be used to get at the member of a struct referenced by a pointer:

```
struct medal_count {
char* country;
int gold;
int silver;
int bronze;
}

struct medal_count spain = { "Spain", 3, 7 4 };
struct medal_count *winner = &spain;
printf("The winner is %s with %d gold medals", (*winner).country, (*winner).gold);
```

*ptr->mem* is a shortcut for *(\*ptr).mem*:

```
printf("The winner (%s) earned %d silver medals", winner->country, winner->silver);
```



# [C Preprocessor Macros](http://hyperpolyglot.org/c#cpp-macros)

- <https://gcc.gnu.org/onlinedocs/cpp/>



# [Net and Web](http://hyperpolyglot.org/c#net-web)



## [http get](http://hyperpolyglot.org/c#http-get)

How to make an HTTP GET request.



# [Unit Tests](http://hyperpolyglot.org/c#unit-tests)



## [example](http://hyperpolyglot.org/c#unit-test-example)



# [Debugging and Profiling](http://hyperpolyglot.org/c#debugging-profiling)



# [C](http://hyperpolyglot.org/c#top)

[ANSI C Standard (pdf)](http://www.open-std.org/jtc1/sc22/WG14/www/docs/n1256.pdf) 1999
[GNU C Library](http://www.gnu.org/software/libc/manual/html_mono/libc.html)

```
FREQUENTLY USED GCC and CLANG OPTIONS

-o name of output file

TYPE OF BUILD

-E  stop after preprocessor; do not compile
-S  stop after compilation; do not assemble
-c  stop after assembly; do not link

PREPROCESSOR

-I          add directory to list of directories containing header files
-D FOO      define macro FOO as 1
-D FOO=VAL  define macro FOO as VAL
-U FOO      undefine macro FOO
-M          output make dependency info

LINKER

-lfoo  search library foo for symbols when liking
-L     add directory to search path used by -l

WARNINGS

-w       no warnings
-Werror  make warnings errors
-Wall    enable all warnings

DEBUGGING, PROFILING, and OPTIMIZATION

-g           make object debuggable
-pg          generate executable which produces output for gprof
-O1 -O2 -O2  spend progressively more time in compilation optimizing code

MAC SPECIFIC

-F  add a framework directory (used in place of -I, -l, -L)
```



# [Go](http://hyperpolyglot.org/c#top)

[Language Specification](http://golang.org/doc/go_spec.html)
[Package Reference](http://golang.org/pkg/)

[issue tracker](https://github.com/clarkgrubb/hyperpolyglot/issues) | content of this page licensed under [creative commons attribution-sharealike 3.0](http://creativecommons.org/licenses/by-sa/3.0/) 