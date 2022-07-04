## 判断C语言的版本

 可以通过宏 __STDC_VERSION__ 来判断

 ```c
#include <stdio.h>

int main()
{
    printf("STDC_VERSION:%ld\n", __STDC_VERSION__ );
    return 0;
}
 ```



| 版本     | `__STDC_VERSION__` |
| -------- | ------------------ |
| C99前    | 不支持该宏         |
| C99      | 199901             |
| C11      | 201112             |
| C18(C17) | 201710             |





## gcc 编译选项

[GCC 编译及编译选项_浩世轩宇的博客-CSDN博客gcc编译选项](https://blog.csdn.net/luguifang2011/article/details/80642692?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-80642692-blog-19811407.pc_relevant_antiscanv3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~Rate-1-80642692-blog-19811407.pc_relevant_antiscanv3&utm_relevant_index=2)

[gcc编译选项_帝都码农的博客-CSDN博客_gcc编译器的选项](https://blog.csdn.net/rheostat/article/details/19811407)