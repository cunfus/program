# 标准库

C 标准库提供了许多函数，用于各种操作和功能。根据功能的不同，这些库函数可以分为以下几类：

### 1. **输入输出函数**

- **标准输入输出**：
  - `printf()`, `scanf()`
  - `fprintf()`, `fscanf()`
  - `sprintf()`, `sscanf()`
  - `vprintf()`, `vscanf()`
  
- **文件操作**：
  - `fopen()`, `fclose()`
  - `fread()`, `fwrite()`
  - `fseek()`, `ftell()`
  - `fprintf()`, `fscanf()`
  - `feof()`, `ferror()`, `clearerr()`

### 2. **字符串处理函数**

- **基本字符串操作**：
  - `strlen()`, ~~`strcpy()`, `strncpy()`~~ -> memcpy
  - ~~`strcat()`, `strncat()`~~ -> memcpy
  - `strcmp()`, `strncmp()`
  - `strchr()`, `strrchr()`
  - `strstr()`, `strtok()`

- **字符串转换**：
  - `atoi()`, `atol()`, `atoll()`
  - `strtol()`, `strtoul()`
  - `strtod()`, `strtof()`, `strtold()`

### 3. **内存管理函数**

- **动态内存分配**：
  - `malloc()`, `calloc()`
  - `realloc()`, `free()`

- **内存操作**：
  - `memcpy()`, `memmove()`
  - `memcmp()`, `memset()`

### 4. **数学函数**

- **基本数学运算**：
  - `abs()`, `fabs()`
  - `pow()`, `sqrt()`, `exp()`, `log()`
  - `sin()`, `cos()`, `tan()`

- **其他数学函数**：
  - `ceil()`, `floor()`, `fmod()`
  - `round()`, `trunc()`, `hypot()`

### 5. **时间和日期函数**

- **时间获取**：
  - `time()`, `localtime()`, `gmtime()`
  - `mktime()`, `strftime()`

- **时间测量**：
  - `clock()`, `difftime()`
  - `clock_gettime()`, `clock_getres()`

### 6. **标准库辅助函数**

- **环境和进程控制**：
  - `exit()`, `atexit()`
  - `getenv()`, `putenv()`

- **错误处理**：
  - `perror()`, `strerror()`

### 7. **类型限定符**

- **限制类型功能**：
  - `sizeof()`, `alignof()`

### 8. **其他功能**

- **断言**：
  - `assert()`

- **临时文件**：
  - `tmpfile()`, `tmpnam()`
