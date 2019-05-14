runtime pkg 里面的stop-the-world STW 是什么意思：停止所有协程的执行，等待GC的回收

GOMAXPROCS变量限制可以同时执行用户级go代码的操作系统线程数。go代码的系统调用中可以阻止的线程数没有限制；这些线程不计入GOMAXPROCS限制。runtime pkg中的GOMAXPROCS函数可以查询和修改这个限制。

GOTRACEBACK变量控制GO程序因未恢复的死机或因意外的运行时条件而失败时生成的输出量。默认情况下，失败打印当前goroutine的堆栈跟踪，删除运行时系统内部的函数，然后退出，退出代码为2。如果没有当前的goroutine或者故障是运行时内部的，那么故障将打印所有goroutine的堆栈跟踪。

- GOTRACEBACK=none : 完全忽略goroutine栈跟踪。

- GOTRACEBACK=single : 行为和上面一样，这个是默认选项。

- GOTRACEBACK=all : 为所有用户创建的goroutine创建栈追踪。

- GOTRACEBACK=system ：类似于"all",但为运行时函数添加堆栈帧，并显示由运行时内部创建的goroutine。

- GOTRACEBACK=crash ：类似于 “GOTRACEBACK=system ”，但以操作系统指定的方式crash而不是exit。

  ​	例如，在UNIX系统上，crash raises SIGABRT 去引发 core dump

  ​	出于历史原因，GOTRACEBACK设置0，1，2分别是none,all,system的同义词。

  ​	runtime/debug 包的SetTraceback 函数允许在运行阶段增加输出量，但是它不能将输出量减少到环境变量指定的量	以下。

编译器是编译运行的二进制文件的编译器工具链的名称。已知的工具链包括：

```
gc      Also known as cmd/compile.
gccgo   The gccgo front end, part of the GCC compiler suite.

const Compiler = "gc"
```

GOARCH is the running program's architecture target: one of 386, amd64, arm, s390x, and so on.

```
const GOARCH string = sys.GOARCH
```

GOOS is the running program's operating system target: one of darwin, freebsd, linux, and so on. To view possible combinations of GOOS and GOARCH, run "go tool dist list".

```
const GOOS string = sys.GOOS
```

memprofilerate 控制在内存配置文件中记录和报告的内存分配比例。探查器的目标是对每个分配的memprofilerate字节进行一次平均分配的采样。

## caller : 

caller 报告有关调用goroutine堆栈上函数调用的文件和行号信息。参数skip是要提升的堆栈帧数，0标识调用方的调用方。（由于历史原因，调用方和调用方之间跳过的含义不同。）返回值报告相应调用文件中的程序计数器、文件名和行号。如果无法恢复信息，则布尔值 ok 为假。

## callers:

callers 用调用goroutine堆栈上函数调用的返回程序计数器填充slice pc。参数skip是在PC中录制之前要跳过的堆栈帧数，0标识调用者本身的帧，1标识调用者的调用者。它返回写入PC的条目数。
要将这些PC转换成符号信息，如函数名和行号，请使用CallersFrames。CallersFrames负责内联函数，并将返回程序计数器调整为调用程序计数器。不鼓励直接遍历返回的PC片，就像在任何返回的PC上使用funcfrpc一样，因为这些不能解释内联或返回程序计数器调整。No线