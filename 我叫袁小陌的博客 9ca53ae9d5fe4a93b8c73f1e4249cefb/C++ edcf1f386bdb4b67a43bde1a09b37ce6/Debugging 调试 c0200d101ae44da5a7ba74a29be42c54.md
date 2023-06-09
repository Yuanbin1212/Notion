# Debugging 调试

Date: May 26, 2023
Last edited time: May 26, 2023 1:44 PM
Level: 二级标题
Owner: 我叫袁小陌
Tags: C++

## G++和GDB的区别

g++ 是 GNU C++ 编译器，用于将 C++ 代码编译为可执行文件。gdb 是 GNU 调试器，允许开发人员在程序崩溃或产生其他问题时跟踪和调试正在运行的程序。以下是有关如何使用 g++ 和 gdb 的简要说明：

## 使用 g++

1. 安装 g++：如果您尚未安装 g++，则需要先安装它。在 Linux 上，可以使用包管理器安装 g++。例如，在 Ubuntu 上，可以使用以下命令安装 g++：

```
sudo apt-get install g++
```

1. 编写源代码：编写 C++ 源代码并将其保存到文件中。
2. 编译代码：打开终端并导航到包含源代码文件的目录中。然后使用以下命令编译代码：

```
g++ -o output_file source_file.cpp

```

其中，output_file 是编译后生成的可执行文件的名称，source_file.cpp 是要编译的源代码文件的名称。

1. 运行可执行文件：使用以下命令运行可执行文件：

```
./output_file
```

以下是常见的 g++ 编译参数：

- `c`：编译源文件但不链接
- `o <file>`：指定输出文件名
- `g`：生成调试信息，方便调试程序
- `Wall`：打开所有警告标志，建议在编译时使用
- `O2`：开启优化选项，提高代码运行速度
- `std=c++11/c++14/c++17`：指定 C++ 标准版本
- `I <dir>`：添加头文件搜索路径
- `L <dir>`：添加库文件搜索路径
- `l <library>`：链接指定库文件

例如，编译 `main.cpp` 并生成可执行文件 `myprog`，可以使用以下命令：

```bash
g++ -std=c++11 -Wall -O2 main.cpp -o myprog
```

## 使用 gdb

1. 安装 gdb：如果您尚未安装 gdb，需要先安装它。在 Linux 上，可以使用包管理器安装 gdb。例如，在 Ubuntu 上，可以使用以下命令安装 gdb：

```bash
sudo apt-get install gdb

```

1. 编译代码：请按照上面的步骤使用 g++ 编译您的代码。确保在编译时添加 -g 选项以生成调试信息。

```bash
g++ -o output_file source_file.cpp -g

```

1. 启动 gdb：打开终端并导航到包含可执行文件的目录中。然后使用以下命令启动 gdb：

```
gdb ./output_file

```

以下是 gdb 常用指令：

- `breakpoint (b)`：在给定的源文件行数、函数名或内存地址处设置断点
- `run (r)`：开始程序的执行
- `print (p)`：打印变量的值或表达式的结果
- `next (n)`：单步执行一行代码（不进入函数）
- `step (s)`：单步执行一行代码（如果有函数调用则进入函数）
- `continue (c)`：继续执行程序直到下一个断点
- `info (i)`：显示程序状态信息，例如堆栈帧和寄存器内容
- `backtrace (bt)`：显示当前线程的完整调用堆栈
- `finish`：执行当前函数并返回
- `watch`：监视变量的值，当其发生改变时中断程序
- `set`：设置变量的值或运行环境参数
- `display`：重复打印表达式的值，每次停在断点时都会打印
- `list`：查看源码上下文
- `delete`：删除断点
- `quit (q)`：退出 gdb