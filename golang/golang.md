main函数保存在名为main的包里。如果main函数不在main包里，构建工具就不会生成可执行的文件
go语言的每个代码文件都属于一个包,main.go也不例外。
一个包定义一组编译过的代码，包的名字类似命名空间，可以用来间接访问包内声明的标识符。这个特性可以把不同包中定义的同名标识符区别开。

所有处于同一个文件夹里的代码文件，必须使用同一个包名。按照惯例，包和文件夹同名。就像之前说的，一个包定义一组编译后的代码，每段代码都描述包的一部分。

与第三方包不同，从标准库中导入代码时，只需要给出要导入的包名。编译器查找包的时候，
总是会到 GOROOT 和 GOPATH 环境变量（如代码清单 2-9 所示）引用的位置去查找。

log 包提供打印日志信息到标准输出（stdout）、标准错误（stderr）或者自定义设备的
功能。

sync 包提供同步 goroutine 的功能。

变量没有定义在任何函数作用域内，所以会被当成包级变量。

在 Go 语言里，标识符要么从包里公开，要么不从包里公开。当代码导入了一个包时，程序
可以直接访问这个包中任意一个公开的标识符。这些标识符以大写字母开头。以小写字母开头的
标识符是不公开的，不能被其他包中的代码直接访问。但是，其他包可以间接访问不公开的标识
符。例如，一个函数可以返回一个未公开类型的值，那么这个函数的任何调用者，哪怕调用者不
是在这个包里声明的，都可以访问这个值。

map 是 Go 语言里的一个引用类型，需要使用 make 来构造。如果不先构造 map 并将构造后
的值赋值给变量，会在试图使用这个 map 变量时收到出错信息。这是因为 map 变量默认的零值
是 nil。在第 4 章我们会进一步了解关于映射的细节。

在 Go 语言中，所有变量都被初始化为其零值。对于数值类型，零值是 0；对于字符串类型，
零值是空字符串；对于布尔类型，零值是 false；对于指针，零值是 nil。对于引用类型来说，
所引用的底层数据结构会被初始化为对应的零值。但是被声明为其零值的引用类型的变量，会返
回 nil 作为其值。

不仅仅是Go语言，很多语言都允许一个函数返回多个值。一般会像RetrieveFeeds函数这
样声明一个函数返回一个值和一个错误值。如果发生了错误，永远不要使用该函数返回的另一个
值，否则程序会产生更多的错误，甚至崩溃。

在第 20 行，我们使用内置的 make 函数创建了一个无缓冲的通道。我们使用简化变量声明
运算符，在调用 make 的同时声明并初始化该通道变量。根据经验，如果需要声明初始值为零值
的变量，应该使用 var 关键字声明变量；如果提供确切的非零值初始化变量或者使用函数返回
值创建变量，应该使用简化变量声明运算符。

在 Go 语言中，通道（channel）和映射（map）与切片（slice）一样，也是引用类型，不过
通道本身实现的是一组带类型的值，这组值用于在 goroutine 之间传递数据。通道内置同步机制，
从而保证通信安全。

在 Go 语言中，如果 main 函数返回，整个程序也就终止了。Go 程序终止时，还会关闭所有
之前启动且还在运行的 goroutine。写并发程序的时候，最佳做法是，在 main 函数返回前，清理
并终止所有之前启动的 goroutine。编写启动和终止时的状态都很清晰的程序，有助减少 bug，防
止资源异常。
这个程序使用 sync 包的 WaitGroup 跟踪所有启动的 goroutine。非常推荐使用 WaitGroup 来
跟踪 goroutine 的工作是否完成。WaitGroup 是一个计数信号量，我们可以利用它来统计所有的
goroutine 是不是都完成了工作。

指针变量可以方便地在函数之间共享数据。使用指针变量可以让函数访问并修改一个变
量的状态，而这个变量可以在其他函数甚至是其他 goroutine 的作用域里声明。

在 Go 语言中，所有的变量
都以值的方式传递。因为指针变量的值是所指向的内存地址，在函数间传递指针变量，是在传递
这个地址值，所以依旧被看作以值的方式在传递。

命名接口的时候，也需要遵守 Go 语言的命名惯例。如果接口类型只包含一个方法，那么这
个类型的名字以 er 结尾。我们的例子里就是这么做的，所以这个接口的名字叫作 Matcher。如
果接口类型内部声明了多个方法，其名字需要与其行为关联。

如果要让一个用户定义的类型实现一个接口，这个用户定义的类型要实现接口类型里声明的
所有方法。

空结构在创建实例时，不会分配任何内存。这种结构很适合创建没有任何状态的类型。

如果声明函数的时候带有接收者，则意味着声明了一个方法。这个方法会和指定的接收者的
类型绑在一起。在我们的例子里，Search 方法与 defaultMatcher 类型的值绑在一起。这意
味着我们可以使用 defaultMatcher 类型的值或者指向这个类型值的指针来调用 Search 方
法。无论我们是使用接收者类型的值来调用这个方，还是使用接收者类型值的指针来调用这个
方法，编译器都会正确地引用或者解引用对应的值 。

因为大部分方法在被调用后都需要维护接收者的值的状态，所以，一个最佳实践是，将方法
的接收者声明为指针。对于 defaultMatcher 类型来说，使用值作为接收者是因为创建一个
defaultMatcher 类型的值不需要分配内存。由于 defaultMatcher 不需要维护状态，所以
不需要指针形式的接收者。

与直接通过值或者指针调用方法不同，如果通过接口类型的值调用方法，规则有很大不同，
如代码清单 2-38 所示。使用指针作为接收者声明的方法，只能在接口类型的值是一个指针的时
候被调用。使用值作为接收者声明的方法，在接口类型的值为值或者指针时，都可以被调用。

所有的.go 文件，除了空行和注释，都应该在第一行声明自己所属的包。每个包都在一个单
独的目录里。不能把多个包放到同一个目录中，也不能把同一个包的文件分拆到多个不同目录中。
这意味着，同一个目录下的所有.go 文件必须声明同一个包名

在 Go 语言里，命名为 main 的包具有特殊的含义。Go 语言的编译程序会试图把这种名字的
包编译为二进制可执行文件。所有用 Go 语言编译的可执行程序都必须有一个名叫 main 的包。

每个包可以包含任意多个 init 函数，这些函数都会在程序执行开始的时候被调用。所有被
编译器发现的 init 函数都会安排在 main 函数之前执行。init 函数用在设置包、初始化变量
或者其他要在程序运行前优先完成的引导工作。

也可以在指定包的时候使用通配符。3 个点表示匹配所有的字符串。例如，下面的命令会编译
chapter3 目录下的所有包：
go build github.com/goinaction/code/chapter3/...

声明一个包含 5 个元素的整型数组
var array [5]int
一旦声明，数组里存储的数据类型和数组长度就都不能改变了。

在 Go 语言里，数组是一个值。这意味着数组可以用在赋值操作中。变量名代表整个数组，
因此，同样类型的数组可以赋值给另一个数组

数组变量的类型包括数组长度和每个元素的类型。只有这两部分都相同的数组，才是类型相
同的数组，才能互相赋值

编译器会阻止类型不同的数组互相赋值

只要类型一致，就可以将多维数组互相赋值，多维数组的类型包括每一维度的长度以及最终存储在元素中的数据的类型。

切片是一种数据结构，这种数据结构便于使用和管理数据集合。切片是围绕动态数组的概念
构建的，可以按需自动增长和缩小。切片的动态增长是通过内置函数 append 来实现的。这个函
数可以快速且高效地增长切片。还可以通过对切片再次切片来缩小一个切片的大小。因为切片的
底层内存也是在连续块中分配的，所以切片还能获得索引、迭代以及为垃圾回收优化的好处。

切片是一个很小的对象，对底层数组进行了抽象，并提供相关的操作方法。切片有 3 个字段
的数据结构，这些数据结构包含 Go 语言需要操作底层数组的元数据（见图 4-9）。
这 3 个字段分别是指向底层数组的指针、切片访问的元素的个数（即长度）和切片允许增长
到的元素个数（即容量）。

声明一个包含 5 个元素的整型数组
// 用具体值初始化每个元素
array := [5]int{10, 20, 30, 40, 50}

 创建字符串切片
// 其长度和容量都是 5 个元素
slice := []string{"Red", "Blue", "Green", "Yellow", "Pink"}

创建一个整型切片
// 其长度和容量都是 3 个元素
slice := [ ]int{10, 20, 30}

// 创建字符串切片
// 使用空字符串初始化第 100 个元素
slice := []string{99: ""}
记住，如果在[ ]运算符里指定了一个值，那么创建的就是数组而不是切片。只有不指定值
的时候，才会创建切片，如代码清单 4-21 所示。

// 创建有 3 个元素的整型数组
array := [3]int{10, 20, 30}
// 创建长度和容量都是 3 的整型切片
slice := []int{10, 20, 30}

有时，程序可能需要声明一个值为 nil 的切片（也称 nil 切片）。只要在声明时不做任何初
始化，就会创建一个 nil 切片

创建 nil 整型切片
var slice [ ]int
在 Go 语言里，nil 切片是很常见的创建切片的方法。nil 切片可以用于很多标准库和内置
函数。在需要描述一个不存在的切片时，nil 切片会很好用。

利用初始化，通过声明一个切片可以创建一个空切片，如代码清单 4-23 所示。
代码清单 4-23 声明空切片
// 使用 make 创建空的整型切片
slice := make([ ]int, 0)
// 使用切片字面量创建空的整型切片
slice := [ ]int{}

空切片在底层数组包含 0 个元素，也没有分配任何存储空间。想表示空集合时空切片很有用，
例如，数据库查询返回 0 个查询结果时

不管是使用 nil 切片还是空切片，对其调用内置函数 append、len 和 cap 的效果都是
一样的。

切片只能访问到其长度内的元素。试图访问超出其长度的元素将会导致语言运行时异常

与切片的容量相关联的元素只能用于增长切片。在使用这部分元素前，必须
将其合并到切片的长度里

切片有额外的容量是很好，但是如果不能把这些容量合并到切片的长度里，这些容量就没有
用处。好在可以用 Go 语言的内置函数 append 来做这种合并很容易。

关键字 range 总是会从切片头部开始迭代。如果想对迭代做更多的控制，依旧可以使用传
统的 for 循环

和数组一样，切片是一维的。不过，和之前对数组的讨论一样，可以组合多个切片形成多维
切片

在函数间传递切片就是要在函数间以值的方式传递切片。由于切片的尺寸很小，在函数间复
制和传递切片成本也很低。

映射是一种数据结构，用于存储一系列无序的键值对。
映射里基于键来存储值。图 4-23 通过一个例子展示了映射里键值对是如何存储的。映射功
能强大的地方是，能够基于键快速检索数据。键就像索引一样，指向与该键关联的值。

映射是一个集合，可以使用类似处理数组和切片的方式迭代映射中的元素。但映射是无序的
集合，意味着没有办法预测键值对被返回的顺序。即便使用同样的顺序保存键值对，每次迭代映
射的时候顺序也可能不一样。无序的原因是映射的实现使用了散列表

映射的键可以是任何值。这个值的类型可以是内置的类型，也可以是结构类型，只要这个值
可以使用==运算符做比较。切片、函数以及包含切片的结构类型这些类型由于具有引用语义，
不能作为映射的键，使用这些类型会造成编译错误

没有任何理由阻止用户使用切片作为映射的值，如代码清单 4-47 所示。这个在使用一个映射
键对应一组数据时，会非常有用。

可以通过声明一个未初始化的映射来创建一个值为 nil 的映射（称为 nil 映射 ）。nil 映射
不能用于存储键值对，否则，会产生一个语言运行时错误

在 Go 语言里，通过键来索引映射时，即便这个键不存在也总会返回一个值。在这种情况下，
返回的是该值对应的类型的零值。

迭代映射里的所有值和迭代数组或切片一样，使用关键字 range，如代码清单 4-52 所示。
但对映射来说，range 返回的不是索引和值，而是键值对。

如果想把一个键值对从映射里删除，就使用内置的 delete 函数

在函数间传递映射并不会制造出该映射的一个副本。实际上，当传递映射给一个函数，并对
这个映射做了修改时，所有对这个映射的引用都会察觉到这个修改

数组是构造切片和映射的基石。

切片有容量限制，不过可以使用内置的 append 函数扩展容量。

映射的增长没有容量或者任何限制。

内置函数 len 可以用来获取切片或者映射的长度。
内置函数 cap 只能用于切片。

将切片或者映射传递给函数成本很小，并且不会复制底层的数据结构。

Go 语言是一种静态类型的编程语言。这意味着，编译器需要在编译时知晓程序里每个值的
类型。如果提前知道类型信息，编译器就可以确保程序合理地使用值。这有助于减少潜在的内存
异常和 bug，并且使编译器有机会对代码进行一些性能优化，提高执行效率。

任何时候，创建一个变量并初始化为其零值，习惯是使用关键字 var。这种用法是为了更明
确地表示一个变量被设置为零值。如果变量被初始化为某个非零值，就配合结构字面量和短变量
声明操作符来创建变量。

既然要创建并初始化一个结构类型，我们就使用结构字面量来完成这个初始化，如代码清
单 5-4 所示。结构字面量使用一对大括号括住内部字段的初始值。
代码清单 5-4 使用结构字面量创建结构类型的值
13 user{
14 name: "Lisa",
15 email: "lisa@email.com",
16 ext: 123,
17 privileged: true,
18 }

当声明结构类型时，字段的类型并
不限制在内置类型，也可以使用其他用户定义的类型，

当创建具有用户自定义类型字段
的结构类型的变量时，初始化用的结构字面量会有一些变化

另一种声明用户定义的类型的方法是，基于一个已有的类型，将其作为新类型的类型说明。
当需要一个可以用已有类型表示的新类型的时候，这种方法会非常好用，如代码清单 5-8 所示。
标准库使用这种声明类型的方法，从内置类型创建出很多更加明确的类型，并赋予更高级的功能。

代码清单 5-8 展示的是标准库的 time 包里的一个类型的声明。Duration 是一种描述时间
间隔的类型，单位是纳秒（ns）。这个类型使用内置的 int64 类型作为其表示。在 Duration
类型的声明中，我们把 int64 类型叫作 Duration 的基础类型。不过，虽然 int64 是基础
类型，Go 并不认为 Duration 和 int64 是同一种类型。这两个类型是完全不同的有区别的
类型。

编译器很清楚这个程序的问题：类型 int64 的值不能作为类型 Duration 的值来用。换句
话说，虽然 int64 类型是基础类型，Duration 类型依然是一个独立的类型。两种不同类型的
值即便互相兼容，也不能互相赋值。编译器不会对不同类型的值做隐式转换。

方法能给用户定义的类型添加新的行为。方法实际上也是函数，只是在声明时，在关键字
func 和方法名之间增加了一个参数，如代码清单 5-11 所示。

关键字 func 和函数名之间的
参数被称作接收者，将函数与接收者的类型绑在一起。如果一个函数有接收者，这个函数就被称
为方法。

Go 语言里有两种类型的接收者：值接收者和指针接收者。

值接收者使用
值的副本来调用方法，而指针接受者使用实际值来调用方法。

如果一个创建用的工厂函数返回了一
个指针，就表示这个被返回的值的本质是非原始的。

代码清单 5-33 中的 Chdir 方法展示了，即使没有修改接收者的值，依然是用指针接收者来
声明的。因为 File 类型的值具备非原始的本质，所以总是应该被共享，而不是被复制。
是使用值接收者还是指针接收者，不应该由该方法是否修改了接收到的值来决定。这个决策
应该基于该类型的本质。这条规则的一个例外是，需要让类型值符合某个接口的时候，即便类型
的本质是非原始本质的，也可以选择使用值接收者声明方法。这样做完全符合接口值调用方法的
机制。

要嵌入一个类型，只需要声明这个类型的名字就可以了。注意声明字段和嵌入类型在语法上的不同。

这表明，如果外部类型
实现了 notify 方法，内部类型的实现就不会被提升。不过内部类型的值一直存在，因此还可以
通过直接访问内部类型的值，来调用没有被提升的内部类型实现的方法。

当要
写的代码属于某个包时，好的实践是使用与代码所在文件夹一样的名字作为包名。所有的 Go 工
具都会利用这个习惯，所以最好遵守这个好的实践。

当一个标识符的名字以小写字母开头时，这个标识符就是未公开的，即包外的代码不可见。
如果一个标识符以大写字母开头，这个标识符就是公开的，即被包外的代码可见。

将工厂函数命名为 New 是 Go 语言的一个习惯。

方法提供了一种给用户定义的类型增加行为的方式。
设计类型时需要确认类型的本质是原始的，还是非原始的。

接口是声明了一组行为并支持多态的类型。

嵌入类型提供了扩展类型的能力，而无需使用继承。

标识符要么是从包里公开的，要么是在包里未公开的。

需要强调的是，使用多个逻辑处理器并不意味着性能更好。在修改任何语言运行时配置参数
的时候，都需要配合基准测试来评估程序的运行效果。

对一个共享资源的读和写操作必
须是原子化的，换句话说，同一时刻只能有一个 goroutine 对共享资源进行读和写操作。

当通道关闭后，goroutine 依旧可以从通道接收数据，
但是不能再向通道里发送数据。能够从已经关闭的通道接收数据这一点非常重要，因为这允许通
道关闭后依旧能取出其中缓冲的全部值，而不会有数据丢失。从一个已经关闭且没有数据的通道
里获取数据，总会立刻返回，并返回一个通道类型的零值。如果在获取通道时还加入了可选的标
志，就能得到通道的状态信息。

可以使用通道来控制程序的生命周期。

带 default 分支的 select 语句可以用来尝试向通道发送或者接收数据，而不会阻塞。

有缓冲的通道可以用来管理一组可复用的资源。

语言运行时 (runtime) 会处理好通道的协作和同步。

使用无缓冲的通道来创建完成工作的 goroutine 池。

任何时间都可以用无缓冲的通道来让两个 goroutine 交换数据，在通道操作完成时一定保
证对方接收到了数据。

一个类型可以自由的使用另一个满足相同接口的类型来进行替换被称作可替换性(LSP里氏替换)。这是一个面向对象的特征。

golang中的方法是作用在指定的数据类型上的（即：和指定的数据类型绑定），因此自定义类型，都可以有方法，而不仅仅是struct

方法的声明和调用

type A struct{

​	Num int

}

func (a A) test(){

​	fmt.Println(a.Num);

} 	// 表示A结构体有一个方法，方法名为test , a(A)体现test方法是个A类型绑定的 ，test方法只能通过Person类型来调用，而不能直接调用，也不能使用其他类型变量来调用

对于普通函数，接受者为值类型时，不能将指针类型的数据直接传递；接受者为指针类型时，不能将值类型的数据直接传递。

而对于方法，接受者为值类型时，可以传递指针类型的数据；接受者为指针类型时，可以传递值类型的数据。注意：不管是指针类型还是值类型，在这里统统都是看方法所属类型的类型，如果方法所属类型的类型值，那么就永远是值拷贝，如果方法所属类型是指针，那么永远是引用传递。

golang的结构体没有构造函数，通常可以使用工厂模式来解决这个问题。如果工厂模式中的new函数里面的字段也是小写开头该咋办呢？答案：我们可以再另外提供一个方法。

golang封装的实现步骤
1) 将结构体，字段（属性）的首字母小写（不能导出了，其他包不能使用，类似private)

2) 给结构体所在包提供一个工厂模式的函数，首字母大写。类似一个构造函数

3）提供一个首字母大写的Set方法（类似其他语言的public), 用于对属性判断并赋值

​	func(var 结构体类型名) SetXxx(参数列表)（返回值列表）{

​	//加入数据验证的业务逻辑

​	var 字段 = 参数

​	}

4）提供一个首字母大写的Get方法（类似其他语言的public），用于获取属性的值

​	func (var 结构体类型名) GetXxx(){

​		return var 字段；

​	}

特别说明：在Golang开发中并没有特别强调封装，这点并不像java,所以提醒学过java的朋友，不要总是用java的语法特性来看待Golang, Golang 本身对面向对象的特性做了简化的。

继承可以解决代码复用，让我们的编程更加靠近人类思维。

当多个结构体存在相同属性（字段）和方法时，可以从这些结构体中抽象出结构体（比如刚才的Student) ，在该结构体中定义这些相同的属性（字段）和方法。

其他的结构体不需要重新定义这些属性和方法，只需嵌套一个Student匿名结构体即可。

也就是说：在Golang中，如果一个struct嵌套了另一个匿名结构体，那么这个结构体可以直接访问匿名结构体的字段和方法，从而实现了继承特性。 

 嵌套匿名结构体的基本语法：

​	type Goods struct {

​		Name string

​		Price int

​	}

​	type Book struct {

​		Goods   	// 这里就是嵌套匿名结构体 ，此时Book就相当于拥有了Name 和 Price 两个字					段

​		Writer string

​	}

​	继承的深入讨论

​	1）结构体可以使用嵌套匿名结构体所有的字段和方法，即：首字母大写或者首字母小写的字段和方法都可以使用。

​	2）匿名结构体字段访问可以简化。

​	3）当结构体和匿名结构体有相同的字段或者方法时，编译器采用就近访问原则访问，如果希望访问匿名结构体的字	段和方法，可以通过匿名结构体名来区分。

​	4）结构体嵌入两个（或多个）匿名结构体，例如两个匿名结构体有相同的字段和方法（同时结构体本身没有同名的	字段和方法），在访问时，就必须明确指定匿名结构体名字，否则编译报错。

​	5）如果一个struct嵌套了一个有名结构体，这种模式就是组合，如果是组合关系，那么在访问组合的结构体的字段或	方法时，必须带上结构体的名字

​	6）嵌套匿名结构体后，也可以在创建结构体变量（实例）时，直接指定各个匿名结构体字段的值。如下

​		tv := TV { Goods {"电视剧001"，5000}，Brand {“海尔”，“山东”} }

​	结构体的匿名字段可以是基本数据类型，比如Int等，但是不能重复。

多重继承

​	如果一个struct嵌套了多个匿名结构体，那么该结构体可以直接访问嵌套的匿名结构体的字段和方法，从而实现了多	重继承。

​	如果嵌入的匿名结构体有相同的字段和方法名，则在访问时，需要通过匿名结构体类型名来区分。

​	为了保证代码的简洁性，建议大家尽量不适用多重继承。

接口（Interface）

​	interface类型可以定义一组方法，但是这些不需要实现。并且Interface不能包含任何变量。到某个自定义类型（比如	结构体Phone）要使用的时候，再根据具体情况把这些方法写出来。

​	接口说明：

​		1）接口里的所有方法都没有方法体，即接口的方法都是没有实现的方法。接口体现了程序设计的多态和高内聚	和低耦合思想

​		2）Golang中的接口，不需要显示的实现。只要一个变量，含有接口类型中的所有方法，那么这个变量就实现了	这个接口。因此，Golang中没有implement这样的关键字。

​	接口的注意事项和细节

​		1）接口本身不能创建实例，但是可以指向一个实现了该接口的自定义类型的变量（实例）

​		2）接口中所有的方法都没有方法体，即都是没有实现的方法。

​		3）在Golang中，一个自定义类型需要将某个接口的所有方法都实现，我们才说这个自定义类型实现了该接口。

​		4）一个自定义类型只有实现了某个接口，才能将该自定义类型的实例（变量）赋给接口类型。

​		5）只要是自定义数据类型，就可以实现接口，不仅仅是结构体类型。

​		6）一个自定义类型可以实现多个接口

​		7）Golang接口中不能有任何变量，只能有方法。

​		8）一个接口（比如A接口）可以继承多个别的接口（比如B,C接口），这时如果要实现A接口，也必须将B，C			接口的方法也全部实现

​			// Golang是基于方法来实现接口的

​		9）interface 类型默认是一个指针（引用类型），如果没有对interface初始化就使用，那么会输出nil

​		10) 空接口interface{} 没有任何方法，所以所有类型都实现了空接口，即我们可以把任何一个变量赋给空接口

​	当A结构体继承了B结构体，那么A结构就自动继承了B结构体的字段和方法，并且可以直接使用

​	当A结构体需要扩展功能，同时不希望去破坏继承关系，则可以去实现某个接口即可。因此我们可以认为，实现接口	是对继承机制的补充。

​	实现接口 VS 继承

​	接口和继承解决的问题不同

​		继承的价值主要在于：解决代码的复用性和可维护性。

​		接口的价值主要在于：设计，设计好各种规范（方法），让其他自定义类型去实现这些方法。

​	接口比继承更加灵活

​		接口比继承更加灵活，继承是满足 is - a的关系，而接口只需满足like - a的关系。

​	接口在一定程度上实现代码解耦

​	接口体现多态特征

​		1）多态参数

​		在前面的Usb接口案例，Usb usb，即可以接受手机变量，又可以接受相机变量，就体现了Usb接口多态

​		2）多态数组

​		演示一个案例：给Usb数组中，存放Phone结构体和Camera结构体变量，Phone还有一个特有的方法call(),请遍		历usb数组，如果是Phone变量，除了调用Usb接口声明的方法外，还需要调用Phone特有方法call. ->需要类型		断言 

​	在进行类型断言时，如果类型不匹配，就会报panic，因此进行类型断言时，要确保原来的空接口指向的就是要断言	的类型

​	如何在进行断言时，带上检测机制，如果成功就OK，否则也不要报panic

Golang数据结构与算法

​	1）稀疏数组

​		基本介绍

​		当一个数组中大部分元素为0，或者为同一个值的数组时，可以使用稀疏数组来保存该数组。

​		稀疏数组的处理方法是：

​		1）记录数组一共有几行几列，有多少个不同的值

​		2）把具有不同值的元素的行列及值记录在一个小规模的数组中，从而缩小程序的规模



在golang中，`array`和`struct`都是值类型的，而`slice`、`map`、`chan`是引用类型，所以我们写代码的时候，基本不使用`array`，而是用`slice`代替它，对于`struct`则尽量使用指针，这样避免传递变量时复制数据的时间和空间消耗，也避免了无法修改原数据的情况。

所以想要顺利的使用map，一定要使用内建函数make函数进行创建：

```go
m := make(map[string]string)
```

使用字面量的方式也是可以的，效果同make：

```go
m := map[string]string{}
```



golang中`for range`语法非常方便，可以轻松的遍历`array`、`slice`、`map`等结构，但是它有一个特点，就是会在遍历时把当前遍历到的元素，复制给内部变量

在`for range`内部只需读取数据而不需要修改的情况下，随便怎么写也无所谓，顶多就是代码不够完美，而需要修改数据时，则最好传递`struct`指针

main函数不能有参数和返回值！

```
Currently, it is:
	gc # @#s #%: #+#+# ms clock, #+#/#/#+# ms cpu, #->#-># MB, # MB goal, # P
where the fields are as follows:
	gc #        the GC number, incremented at each GC
	@#s         time in seconds since program start
	#%          percentage of time spent in GC since program start
	#+...+#     wall-clock/CPU times for the phases of the GC
	#->#-># MB  heap size at GC start, at GC end, and live heap
	# MB goal   goal heap size
	# P         number of processors used
		
Currently it is:
	scvg#: # MB released  printed only if non-zero
	scvg#: inuse: # idle: # sys: # released: # consumed: # (MB)
where the fields are as follows:
	scvg#        the scavenge cycle number, incremented at each scavenge
	inuse: #     MB used or partially used spans
	idle: #      MB spans pending scavenging
	sys: #       MB mapped from the system
	released: #  MB released to the system
	consumed: #  MB allocated from the system
```

```go
vname1, vname2, vname3 := v1, v2, v3
```

现在是不是看上去非常简洁了？`:=`这个符号直接取代了`var`和`type`,这种形式叫做简短声明。不过它有一个限制，那就是它只能用在函数内部；在函数外部使用则会无法编译通过，所以一般用`var`方式来定义全局变量。

`_`（下划线）是个特殊的变量名，任何赋予它的值都会被丢弃。在这个例子中，我们将值`35`赋予`b`，并同时丢弃`34`：

```go
_,b := 34, 35
```

## 常量

所谓常量，也就是在程序编译阶段就确定下来的值，而程序在运行时无法改变该值。在Go程序中，常量可定义为数值、布尔值或字符串等类型。

它的语法如下：

```go
const constantName = value
//如果需要，也可以明确指定常量的类型：
const Pi float32 = 3.1415926
```

Go 常量和一般程序语言不同的是，可以指定相当多的小数位数(例如200位)， 若指定給float32自动缩短为32bit，指定给float64自动缩短为64bit，详情参考[链接](http://golang.org/ref/spec#Constants)

### 数值类型

整数类型有无符号和带符号两种。Go同时支持`int`和`uint`，这两种类型的长度相同，但具体长度取决于不同编译器的实现。Go里面也有直接定义好位数的类型：`rune`, `int8`, `int16`, `int32`, `int64`和`byte`, `uint8`, `uint16`, `uint32`, `uint64`。其中`rune`是`int32`的别称，`byte`是`uint8`的别称。

> 需要注意的一点是，这些类型的变量之间不允许互相赋值或操作，不然会在编译时引起编译器报错。
>
> 如下的代码会产生错误：invalid operation: a + b (mismatched types int8 and int32)
>
> var a int8
>
> var b int32
>
> c:=a + b
>
> 另外，尽管int的长度是32 bit, 但int 与 int32并不可以互用。

浮点数的类型有`float32`和`float64`两种（没有`float`类型），默认是`float64`。

### 字符串

我们在上一节中讲过，Go中的字符串都是采用`UTF-8`字符集编码。字符串是用一对双引号（`""`）或反引号（``` ```）括起来定义，它的类型是`string`。

```go
//示例代码
var frenchHello string  // 声明变量为字符串的一般方法
var emptyString string = ""  // 声明了一个字符串变量，初始化为空字符串
func test() {
    no, yes, maybe := "no", "yes", "maybe"  // 简短声明，同时声明多个变量
    japaneseHello := "Konichiwa"  // 同上
    frenchHello = "Bonjour"  // 常规赋值
}
```

在Go中字符串是不可变的，例如下面的代码编译时会报错：cannot assign to s[0]

```go
var s string = "hello"
s[0] = 'c'
```

但如果真的想要修改怎么办呢？下面的代码可以实现：

```go
s := "hello"
c := []byte(s)  // 将字符串 s 转换为 []byte 类型
c[0] = 'c'
s2 := string(c)  // 再转换回 string 类型
fmt.Printf("%s\n", s2)
```

Go中可以使用`+`操作符来连接两个字符串：

```go
s := "hello,"
m := " world"
a := s + m
fmt.Printf("%s\n", a)
```

修改字符串也可写为：

```go
s := "hello"
s = "c" + s[1:] // 字符串虽不能更改，但可进行切片操作
fmt.Printf("%s\n", s)
```

如果要声明一个多行的字符串怎么办？可以通过```来声明：

```go
m := `hello
    world`
```

`括起的字符串为Raw字符串，即字符串在代码中的形式就是打印时的形式，它没有字符转义，换行也将原样输出。例如本例中会输出：

```
hello
    world
```

### 错误类型

Go内置有一个`error`类型，专门用来处理错误信息，Go的`package`里面还专门有一个包`errors`来处理错误：

```go
err := errors.New("emit macho dwarf: elf header corrupted")
if err != nil {
    fmt.Print(err)
}
```

### Go数据底层的存储

下面这张图来源于[Russ Cox Blog](http://research.swtch.com/)中一篇介绍[Go数据结构](http://research.swtch.com/godata)的文章，大家可以看到这些基础类型底层都是分配了一块内存，然后存储了相应的值。

![](C:\Users\y5039\Pictures\Camera Roll\2.2.basic.png)

### 分组声明

在Go语言中，同时声明多个常量、变量，或者导入多个包时，可采用分组的方式进行声明。

例如下面的代码：

```go
import "fmt"
import "os"

const i = 100
const pi = 3.1415
const prefix = "Go_"

var i int
var pi float32
var prefix string
```

可以分组写成如下形式：

```go
import(
    "fmt"
    "os"
)

const(
    i = 100
    pi = 3.1415
    prefix = "Go_"
)

var(
    i int
    pi float32
    prefix string
)
```

### iota枚举

Go里面有一个关键字`iota`，这个关键字用来声明`enum`的时候采用，它默认开始值是0，const中每增加一行加1：

```go
const(
    x = iota  // x == 0
    y = iota  // y == 1
    z = iota  // z == 2
    w  // 常量声明省略值时，默认和之前一个值的字面相同。这里隐式地说w = iota，因此w == 3。其实上面y和z可同样不用"= iota"
)

const v = iota // 每遇到一个const关键字，iota就会重置，此时v == 0

const ( 
  e, f, g = iota, iota, iota //e=0,f=0,g=0 iota在同一行值相同
)

const （
    a = iota    a=0
    b = "B"
    c = iota    //c=2
    d,e,f = iota,iota,iota //d=3,e=3,f=3
    g //g = 4
）
```

> 除非被显式设置为其它值或`iota`，每个`const`分组的第一个常量被默认设置为它的0值，第二及后续的常量被默认设置为它前面那个常量的值，如果前面那个常量的值是`iota`，则它也被设置为`iota`。

### Go程序设计的一些规则

Go之所以会那么简洁，是因为它有一些默认的行为：

- 大写字母开头的变量是可导出的，也就是其它包可以读取的，是公用变量；小写字母开头的就是不可导出的，是私有变量。
- 大写字母开头的函数也是一样，相当于`class`中的带`public`关键词的公有函数；小写字母开头的就是有`private`关键词的私有函数。

## array、slice、map

### array

`array`就是数组，它的定义方式如下：

```go
var arr [n]type
```

在`[n]type`中，`n`表示数组的长度，`type`表示存储元素的类型。对数组的操作和其它语言类似，都是通过`[]`来进行读取或赋值：

```go
var arr [10]int  // 声明了一个int类型的数组
arr[0] = 42      // 数组下标是从0开始的
arr[1] = 13      // 赋值操作
fmt.Printf("The first element is %d\n", arr[0])  // 获取数据，返回42
fmt.Printf("The last element is %d\n", arr[9]) //返回未赋值的最后一个元素，默认返回0
```

由于长度也是数组类型的一部分，因此`[3]int`与`[4]int`是不同的类型，数组也就不能改变长度。数组之间的赋值是值的赋值，即当把一个数组作为参数传入函数的时候，传入的其实是该数组的副本，而不是它的指针。如果要使用指针，那么就需要用到后面介绍的`slice`类型了。

数组可以使用另一种`:=`来声明

```go
a := [3]int{1, 2, 3} // 声明了一个长度为3的int数组

b := [10]int{1, 2, 3} // 声明了一个长度为10的int数组，其中前三个元素初始化为1、2、3，其它默认为0

c := [...]int{4, 5, 6} // 可以省略长度而采用`...`的方式，Go会自动根据元素个数来计算长度
```

也许你会说，我想数组里面的值还是数组，能实现吗？当然咯，Go支持嵌套数组，即多维数组。比如下面的代码就声明了一个二维数组：

```go
// 声明了一个二维数组，该数组以两个数组作为元素，其中每个数组中又有4个int类型的元素
doubleArray := [2][4]int{[4]int{1, 2, 3, 4}, [4]int{5, 6, 7, 8}}

// 上面的声明可以简化，直接忽略内部的类型
easyArray := [2][4]int{{1, 2, 3, 4}, {5, 6, 7, 8}}
```

数组的分配如下所示：

![](C:\Users\y5039\Pictures\Camera Roll\2.2.array.png)

​																图2.2 多维数组的映射关系

### slice

在很多应用场景中，数组并不能满足我们的需求。在初始定义数组时，我们并不知道需要多大的数组，因此我们就需要“动态数组”。在Go里面这种数据结构叫`slice`

`slice`并不是真正意义上的动态数组，而是一个引用类型。`slice`总是指向一个底层`array`，`slice`的声明也可以像`array`一样，只是不需要长度。

```go
// 和声明array一样，只是少了长度
var fslice []int
```

接下来我们可以声明一个`slice`，并初始化数据，如下所示：

```go
slice := []byte {'a', 'b', 'c', 'd'}
```

`slice`可以从一个数组或一个已经存在的`slice`中再次声明。`slice`通过`array[i:j]`来获取，其中`i`是数组的开始位置，`j`是结束位置，但不包含`array[j]`，它的长度是`j-i`。

```go
// 声明一个含有10个元素元素类型为byte的数组
var ar = [10]byte {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}

// 声明两个含有byte的slice
var a, b []byte

// a指向数组的第3个元素开始，并到第五个元素结束，
a = ar[2:5]
//现在a含有的元素: ar[2]、ar[3]和ar[4]

// b是数组ar的另一个slice
b = ar[3:5]
// b的元素是：ar[3]和ar[4]
```

> 注意`slice`和数组在声明时的区别：声明数组时，方括号内写明了数组的长度或使用`...`自动计算长度，而声明`slice`时，方括号内没有任何字符。

它们的数据结构如下所示：

![](C:\Users\y5039\Pictures\Camera Roll\2.2.slice.png)

​																		图2.3 slice和array的对应关系图

slice有一些简便的操作

- `slice`的默认开始位置是0，`ar[:n]`等价于`ar[0:n]`
- `slice`的第二个序列默认是数组的长度，`ar[n:]`等价于`ar[n:len(ar)]`
- 如果从一个数组里面直接获取`slice`，可以这样`ar[:]`，因为默认第一个序列是0，第二个是数组的长度，即等价于`ar[0:len(ar)]`

下面这个例子展示了更多关于`slice`的操作：

```go
// 声明一个数组
var array = [10]byte{'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}
// 声明两个slice
var aSlice, bSlice []byte

// 演示一些简便操作
aSlice = array[:3] // 等价于aSlice = array[0:3] aSlice包含元素: a,b,c
aSlice = array[5:] // 等价于aSlice = array[5:10] aSlice包含元素: f,g,h,i,j
aSlice = array[:]  // 等价于aSlice = array[0:10] 这样aSlice包含了全部的元素

// 从slice中获取slice
aSlice = array[3:7]  // aSlice包含元素: d,e,f,g，len=4，cap=7
bSlice = aSlice[1:3] // bSlice 包含aSlice[1], aSlice[2] 也就是含有: e,f
bSlice = aSlice[:3]  // bSlice 包含 aSlice[0], aSlice[1], aSlice[2] 也就是含有: d,e,f
bSlice = aSlice[0:5] // 对slice的slice可以在cap范围内扩展，此时bSlice包含：d,e,f,g,h
bSlice = aSlice[:]   // bSlice包含所有aSlice的元素: d,e,f,g
```

`slice`是引用类型，所以当引用改变其中元素的值时，其它的所有引用都会改变该值，例如上面的`aSlice`和`bSlice`，如果修改了`aSlice`中元素的值，那么`bSlice`相对应的值也会改变。

从概念上面来说`slice`像一个结构体，这个结构体包含了三个元素：

- 一个指针，指向数组中`slice`指定的开始位置

- 长度，即`slice`的长度

- 最大长度，也就是`slice`开始位置到数组的最后位置的长度

  ```go
  Array_a := [10]byte{'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}
    Slice_a := Array_a[2:5]
  ```

  上面代码的真正存储结构如下图所示

  ![](C:\Users\y5039\Pictures\Camera Roll\2.2.slice2.png)

  ​													图2.4 slice对应数组的信息

对于`slice`有几个有用的内置函数：

- `len` 获取`slice`的长度
- `cap` 获取`slice`的最大容量
- `append` 向`slice`里面追加一个或者多个元素，然后返回一个和`slice`一样类型的`slice`
- `copy` 函数`copy`从源`slice`的`src`中复制元素到目标`dst`，并且返回复制的元素的个数

注：`append`函数会改变`slice`所引用的数组的内容，从而影响到引用同一数组的其它`slice`。 但当`slice`中没有剩余空间（即`(cap-len) == 0`）时，此时将动态分配新的数组空间。返回的`slice`数组指针将指向这个空间，而原数组的内容将保持不变；其它引用此数组的`slice`则不受影响。

从Go1.2开始slice支持了三个参数的slice，之前我们一直采用这种方式在slice或者array基础上来获取一个slice：

```go
var array [10]int
slice := array[2:4]
```

这个例子里面slice的容量是8，新版本里面可以指定这个容量：

```go
slice = array[2:4:7]
```

上面这个的容量就是`7-2`，即5。这样这个产生的新的slice就没办法访问最后的三个元素。

如果slice是这样的形式`array[:i:j]`，即第一个参数为空，默认值就是0。

### map

`map`也就是Python中字典的概念，它的格式为`map[keyType]valueType` 

我们看下面的代码，`map`的读取和设置也类似`slice`一样，通过`key`来操作，只是`slice`的`index`只能是`int` 类型，而`map`多了很多类型，可以是`int`，可以是`string`及所有完全定义了`==`与`!=`操作的类型。

```go
// 声明一个key是字符串，值为int的字典,这种方式的声明需要在使用之前使用make初始化
var numbers map[string]int
// 另一种map的声明方式
numbers := make(map[string]int)
numbers["one"] = 1  //赋值
numbers["ten"] = 10 //赋值
numbers["three"] = 3

fmt.Println("第三个数字是: ", numbers["three"]) // 读取数据
// 打印出来如:第三个数字是: 3
```

这个`map`就像我们平常看到的表格一样，左边列是`key`，右边列是值

使用map过程中需要注意的几点：

- `map`是无序的，每次打印出来的`map`都会不一样，它不能通过`index`获取，而必须通过`key`获取
- `map`的长度是不固定的，也就是和`slice`一样，也是一种引用类型
- 内置的`len`函数同样适用于`map`，返回`map`拥有的`key`的数量
- `map`的值可以很方便的修改，通过`numbers["one"]=11`可以很容易的把key为`one`的字典值改为`11`
- `map`和其他基本型别不同，它不是thread-safe，在多个go-routine存取时，必须使用mutex lock机制

`map`的初始化可以通过`key:val`的方式初始化值，同时`map`内置有判断是否存在`key`的方式

通过`delete`删除`map`的元素：

```go
// 初始化一个字典
rating := map[string]float32{"C":5, "Go":4.5, "Python":4.5, "C++":2 }
// map有两个返回值，第二个返回值，如果不存在key，那么ok为false，如果存在ok为true
csharpRating, ok := rating["C#"]
if ok {
    fmt.Println("C# is in the map and its rating is ", csharpRating)
} else {
    fmt.Println("We have no rating associated with C# in the map")
}

delete(rating, "C")  // 删除key为C的元素
```

上面说过了，`map`也是一种引用类型，如果两个`map`同时指向一个底层，那么一个改变，另一个也相应的改变：

```go
m := make(map[string]string)
m["Hello"] = "Bonjour"
m1 := m
m1["Hello"] = "Salut"  // 现在m["hello"]的值已经是Salut了
```

### make、new操作

`make`用于内建类型（`map`、`slice` 和`channel`）的内存分配。`new`用于各种类型的内存分配。

内建函数`new`本质上说跟其它语言中的同名函数功能一样：`new(T)`分配了零值填充的`T`类型的内存空间，并且返回其地址，即一个`*T`类型的值。用Go的术语说，它返回了一个指针，指向新分配的类型`T`的零值。有一点非常重要：

> `new`返回指针。

下面这个图详细的解释了`new`和`make`之间的区别。

![](C:\Users\y5039\Pictures\Camera Roll\2.2.makenew.png)

​										图2.5 make和new对应底层的内存分配

## 零值

关于“零值”，所指并非是空值，而是一种“变量未填充前”的默认值，通常为0。 此处罗列 部分类型 的 “零值”

```go
int     0
int8    0
int32   0
int64   0
uint    0x0
rune    0 //rune的实际类型是 int32
byte    0x0 // byte的实际类型是 uint8
float32 0 //长度为 4 byte
float64 0 //长度为 8 byte
bool    false
string  ""
```

## Numeric types

数字类型表示一组整数或浮点值。预先声明的与硬件架构无关的数字类型有：

```go
uint8       the set of all unsigned  8-bit integers (0 to 255)
uint16      the set of all unsigned 16-bit integers (0 to 65535)
uint32      the set of all unsigned 32-bit integers (0 to 4294967295)
uint64      the set of all unsigned 64-bit integers (0 to 18446744073709551615)

int8        the set of all signed  8-bit integers (-128 to 127)
int16       the set of all signed 16-bit integers (-32768 to 32767)
int32       the set of all signed 32-bit integers (-2147483648 to 2147483647)
int64       the set of all signed 64-bit integers (-9223372036854775808 to 9223372036854775807)

float32     the set of all IEEE-754 32-bit floating-point numbers
float64     the set of all IEEE-754 64-bit floating-point numbers

complex64   the set of all complex numbers with float32 real and imaginary parts
complex128  the set of all complex numbers with float64 real and imaginary parts

byte        alias for uint8
rune        alias for int32
```

## 2.3 流程和函数

这小节我们要介绍Go里面的流程控制以及函数操作。

### 流程控制

流程控制在编程语言中是最伟大的发明了，因为有了它，你可以通过很简单的流程描述来表达很复杂的逻辑。Go中流程控制分三大类：条件判断，循环控制和无条件跳转。

### if

`if`也许是各种编程语言中最常见的了，它的语法概括起来就是:如果满足条件就做某事，否则做另一件事。

Go里面`if`条件判断语句中不需要括号，如下代码所示：

```go
if x > 10 {
    fmt.Println("x is greater than 10")
} else {
    fmt.Println("x is less than 10")
}
```

Go的`if`还有一个强大的地方就是条件判断语句里面允许声明一个变量，这个变量的作用域只能在该条件逻辑块内，其他地方就不起作用了，如下所示：

```go
// 计算获取值x,然后根据x返回的大小，判断是否大于10。
if x := computedValue(); x > 10 {
    fmt.Println("x is greater than 10")
} else {
    fmt.Println("x is less than 10")
}

//这个地方如果这样调用就编译出错了，因为x是条件里面的变量
fmt.Println(x)
```

### goto

Go有`goto`语句——请明智地使用它。用`goto`跳转到必须在当前函数内定义的标签。例如假设这样一个循环：

```go
func myFunc() {
    i := 0
Here:   //这行的第一个词，以冒号结束作为标签
    println(i)
    i++
    goto Here   //跳转到Here去
}
```

> 标签名是大小写敏感的。

### for

Go里面最强大的一个控制逻辑就是`for`，它即可以用来循环读取数据，又可以当作`while`来控制逻辑，还能迭代操作。它的语法如下：

```go
for expression1; expression2; expression3 {
    //...
}
```

`expression1`、`expression2`和`expression3`都是表达式，其中`expression1`和`expression3`是变量声明或者函数调用返回值之类的，`expression2`是用来条件判断，`expression1`在循环开始之前调用，`expression3`在每轮循环结束之时调用。

一个例子比上面讲那么多更有用，那么我们看看下面的例子吧：

```go
package main
import "fmt"

func main(){
    sum := 0;
    for index:=0; index < 10 ; index++ {
        sum += index
    }
    fmt.Println("sum is equal to ", sum)
}
// 输出：sum is equal to 45
```

有些时候需要进行多个赋值操作，由于Go里面没有`,`操作符，那么可以使用平行赋值`i, j = i+1, j-1`

有些时候如果我们忽略`expression1`和`expression3`：

```go
sum := 1
for ; sum < 1000;  {
    sum += sum
}
```

其中`;`也可以省略，那么就变成如下的代码了，是不是似曾相识？对，这就是`while`的功能。

```go
sum := 1
for sum < 1000 {
    sum += sum
}
```

其中`;`也可以省略，那么就变成如下的代码了，是不是似曾相识？对，这就是`while`的功能。

```go
sum := 1
for sum < 1000 {
    sum += sum
}
```

在循环里面有两个关键操作`break`和`continue` ,`break`操作是跳出当前循环，`continue`是跳过本次循环。当嵌套过深的时候，`break`可以配合标签使用，即跳转至标签所指定的位置，详细参考如下例子：

```go
for index := 10; index>0; index-- {
    if index == 5{
        break // 或者continue
    }
    fmt.Println(index)
}
// break打印出来10、9、8、7、6
// continue打印出来10、9、8、7、6、4、3、2、1
```

`break`和`continue`还可以跟着标号，用来跳到多重循环中的外层循环

`for`配合`range`可以用于读取`slice`和`map`的数据：

```go
for k,v:=range map {
    fmt.Println("map's key:",k)
    fmt.Println("map's val:",v)
}
```

由于 Go 支持 “多值返回”, 而对于“声明而未被调用”的变量, 编译器会报错, 在这种情况下, 可以使用`_`来丢弃不需要的返回值 例如：

```go
for _, v := range map{
    fmt.Println("map's val:", v)
}
```

### switch

有些时候你需要写很多的`if-else`来实现一些逻辑处理，这个时候代码看上去就很丑很冗长，而且也不易于以后的维护，这个时候`switch`就能很好的解决这个问题。它的语法如下

```go
switch sExpr {
case expr1:
    some instructions
case expr2:
    some other instructions
case expr3:
    some other instructions
default:
    other code
}
```

`sExpr`和`expr1`、`expr2`、`expr3`的类型必须一致。

Go的`switch`非常灵活，表达式不必是常量或整数，执行的过程从上至下，直到找到匹配项；而如果`switch`没有表达式，它会匹配`true`。

```go
i := 10
switch i {
case 1:
    fmt.Println("i is equal to 1")
case 2, 3, 4:
    fmt.Println("i is equal to 2, 3 or 4")
case 10:
    fmt.Println("i is equal to 10")
default:
    fmt.Println("All I know is that i is an integer")
}
```

在第5行中，我们把很多值聚合在了一个`case`里面，同时，Go里面`switch`默认相当于每个`case`最后带有`break`，匹配成功后不会自动向下执行其他case，而是跳出整个`switch`, 但是可以使用`fallthrough`强制执行后面的case代码：

```go
integer := 6
switch integer {
case 4:
    fmt.Println("The integer was <= 4")
    fallthrough
case 5:
    fmt.Println("The integer was <= 5")
    fallthrough
case 6:
    fmt.Println("The integer was <= 6")
    fallthrough
case 7:
    fmt.Println("The integer was <= 7")
    fallthrough
case 8:
    fmt.Println("The integer was <= 8")
    fallthrough
default:
    fmt.Println("default case")
}
```

上面的程序将输出:

```go
The integer was <= 6
The integer was <= 7
The integer was <= 8
default case
```

## 函数

函数是Go里面的核心设计，它通过关键字`func`来声明，它的格式如下：

```go
func funcName(input1 type1, input2 type2) (output1 type1, output2 type2) {
    //这里是处理逻辑代码
    //返回多个值
    return value1, value2
}
```

上面的代码我们看出

- 关键字`func`用来声明一个函数`funcName`
- 函数可以有一个或者多个参数，每个参数后面带有类型，通过`,`分隔
- 函数可以返回多个值
- 上面返回值声明了两个变量`output1`和`output2`，如果你不想声明也可以，直接就两个类型
- 如果只有一个返回值且不声明返回值变量，那么你可以省略 包括返回值 的括号
- 如果没有返回值，那么就直接省略最后的返回信息
- 如果有返回值， 那么必须在函数的外层添加return语句

下面我们来看一个实际应用函数的例子（用来计算Max值）



```go
package main
import "fmt"

// 返回a、b中最大值.
func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func main() {
    x := 3
    y := 4
    z := 5

    max_xy := max(x, y) //调用函数max(x, y)
    max_xz := max(x, z) //调用函数max(x, z)

    fmt.Printf("max(%d, %d) = %d\n", x, y, max_xy)
    fmt.Printf("max(%d, %d) = %d\n", x, z, max_xz)
    fmt.Printf("max(%d, %d) = %d\n", y, z, max(y,z)) // 也可在这直接调用它
}
```

上面这个里面我们可以看到`max`函数有两个参数，它们的类型都是`int`，那么第一个变量的类型可以省略（即 a,b int,而非 a int, b int)，默认为离它最近的类型，同理多于2个同类型的变量或者返回值。同时我们注意到它的返回值就是一个类型，这个就是省略写法。

### 多个返回值

Go语言比C更先进的特性，其中一点就是函数能够返回多个值。

我们直接上代码看例子：

```go
package main
import "fmt"

//返回 A+B 和 A*B
func SumAndProduct(A, B int) (int, int) {
    return A+B, A*B
}

func main() {
    x := 3
    y := 4

    xPLUSy, xTIMESy := SumAndProduct(x, y)

    fmt.Printf("%d + %d = %d\n", x, y, xPLUSy)
    fmt.Printf("%d * %d = %d\n", x, y, xTIMESy)
}
```

上面的例子我们可以看到直接返回了两个参数，当然我们也可以命名返回参数的变量，这个例子里面只是用了两个类型，我们也可以改成如下这样的定义，然后返回的时候不用带上变量名，因为直接在函数里面初始化了。但如果你的函数是导出的(首字母大写)，官方建议：最好命名返回值，因为不命名返回值，虽然使得代码更加简洁了，但是会造成生成的文档可读性差。

```go
func SumAndProduct(A, B int) (add int, Multiplied int) {
    add = A+B
    Multiplied = A*B
    return
}
```



### 变参

Go函数支持变参。接受变参的函数是有着不定数量的参数的。为了做到这点，首先需要定义函数使其接受变参：

```go
func myfunc(arg ...int) {}
```

`arg ...int`告诉Go这个函数接受不定数量的参数。注意，这些参数的类型全部是`int`。在函数体中，变量`arg`是一个`int`的`slice`：

```go
for _, n := range arg {
    fmt.Printf("And the number is: %d\n", n)
}
```

### 传值与传指针

当我们传一个参数值到被调用函数里面时，实际上是传了这个值的一份copy，当在被调用函数中修改参数值的时候，调用函数中相应实参不会发生任何变化，因为数值变化只作用在copy上。

为了验证我们上面的说法，我们来看一个例子：

```go
package main
import "fmt"

//简单的一个函数，实现了参数+1的操作
func add1(a int) int {
    a = a+1 // 我们改变了a的值
    return a //返回一个新值
}

func main() {
    x := 3

    fmt.Println("x = ", x)  // 应该输出 "x = 3"

    x1 := add1(x)  //调用add1(x)

    fmt.Println("x+1 = ", x1) // 应该输出"x+1 = 4"
    fmt.Println("x = ", x)    // 应该输出"x = 3"
}
```

看到了吗？虽然我们调用了`add1`函数，并且在`add1`中执行`a = a+1`操作，但是上面例子中`x`变量的值没有发生变化

理由很简单：因为当我们调用`add1`的时候，`add1`接收的参数其实是`x`的copy，而不是`x`本身。

那你也许会问了，如果真的需要传这个`x`本身,该怎么办呢？

这就牵扯到了所谓的指针。我们知道，变量在内存中是存放于一定地址上的，修改变量实际是修改变量地址处的内存。只有`add1`函数知道`x`变量所在的地址，才能修改`x`变量的值。所以我们需要将`x`所在地址`&x`传入函数，并将函数的参数的类型由`int`改为`*int`，即改为指针类型，才能在函数中修改`x`变量的值。此时参数仍然是按copy传递的，只是copy的是一个指针。请看下面的例子

```go
package main
import "fmt"

//简单的一个函数，实现了参数+1的操作
func add1(a *int) int { // 请注意，
    *a = *a+1 // 修改了a的值
    return *a // 返回新值
}

func main() {
    x := 3

    fmt.Println("x = ", x)  // 应该输出 "x = 3"

    x1 := add1(&x)  // 调用 add1(&x) 传x的地址

    fmt.Println("x+1 = ", x1) // 应该输出 "x+1 = 4"
    fmt.Println("x = ", x)    // 应该输出 "x = 4"
}
```

这样，我们就达到了修改`x`的目的。那么到底传指针有什么好处呢？

- 传指针使得多个函数能操作同一个对象。
- 传指针比较轻量级 (8bytes),只是传内存地址，我们可以用指针传递体积大的结构体。如果用参数值传递的话, 在每次copy上面就会花费相对较多的系统开销（内存和时间）。所以当你要传递大的结构体的时候，用指针是一个明智的选择。
- Go语言中`channel`，`slice`，`map`这三种类型的实现机制类似指针，所以可以直接传递，而不用取地址后传递指针。（注：若函数需改变`slice`的长度，则仍需要取地址传递指针）

## defer

Go语言中有种不错的设计，即延迟（defer）语句，你可以在函数中添加多个defer语句。当函数执行到最后时，这些defer语句会按照逆序执行，最后该函数返回。特别是当你在进行一些打开资源的操作时，遇到错误需要提前返回，在返回前你需要关闭相应的资源，不然很容易造成资源泄露等问题。如下代码所示，我们一般写打开一个资源是这样操作的：

```go
func ReadWrite() bool {
    file.Open("file")
// 做一些工作
    if failureX {
        file.Close()
        return false
    }

    if failureY {
        file.Close()
        return false
    }

    file.Close()
    return true
}
```

我们看到上面有很多重复的代码，Go的`defer`有效解决了这个问题。使用它后，不但代码量减少了很多，而且程序变得更优雅。在`defer`后指定的函数会在函数退出前调用。

```go
func ReadWrite() bool {
    file.Open("file")
    defer file.Close()
    if failureX {
        return false
    }
    if failureY {
        return false
    }
    return true
}
```

如果有很多调用`defer`，那么`defer`是采用后进先出模式，所以如下代码会输出`4 3 2 1 0` 

```go
for i := 0; i < 5; i++ {
    defer fmt.Printf("%d ", i)
}
```

## 函数作为值、类型

在Go中函数也是一种变量，我们可以通过`type`来定义它，它的类型就是所有拥有相同的参数，相同的返回值的一种类型

```go
type typeName func(input1 inputType1 , input2 inputType2 [, ...]) (result1 resultType1 [, ...])
```

函数作为类型到底有什么好处呢？那就是可以把这个类型的函数当做值来传递，请看下面的例子

```go
package main
import "fmt"

type testInt func(int) bool // 声明了一个函数类型

func isOdd(integer int) bool {
    if integer%2 == 0 {
        return false
    }
    return true
}

func isEven(integer int) bool {
    if integer%2 == 0 {
        return true
    }
    return false
}

// 声明的函数类型在这个地方当做了一个参数

func filter(slice []int, f testInt) []int {
    var result []int
    for _, value := range slice {
        if f(value) {
            result = append(result, value)
        }
    }
    return result
}

func main(){
    slice := []int {1, 2, 3, 4, 5, 7}
    fmt.Println("slice = ", slice)
    odd := filter(slice, isOdd)    // 函数当做值来传递了
    fmt.Println("Odd elements of slice are: ", odd)
    even := filter(slice, isEven)  // 函数当做值来传递了
    fmt.Println("Even elements of slice are: ", even)
}
```

函数当做值和类型在我们写一些通用接口的时候非常有用，通过上面例子我们看到`testInt`这个类型是一个函数类型，然后两个`filter`函数的参数和返回值与`testInt`类型是一样的，但是我们可以实现很多种的逻辑，这样使得我们的程序变得非常的灵活。

## Panic和Recover

Go没有像Java那样的异常机制，它不能抛出异常，而是使用了`panic`和`recover`机制。一定要记住，你应当把它作为最后的手段来使用，也就是说，你的代码中应当没有，或者很少有`panic`的东西。这是个强大的工具，请明智地使用它。那么，我们应该如何使用它呢？

Panic

> 是一个内建函数，可以中断原有的控制流程，进入一个令人恐慌的流程中。当函数`F`调用`panic`，函数F的执行被中断，但是`F`中的延迟函数会正常执行，然后F返回到调用它的地方。在调用的地方，`F`的行为就像调用了`panic`。这一过程继续向上，直到发生`panic`的`goroutine`中所有调用的函数返回，此时程序退出。恐慌可以直接调用`panic`产生。也可以由运行时错误产生，例如访问越界的数组。

Recover

> 是一个内建的函数，可以让进入令人恐慌的流程中的`goroutine`恢复过来。`recover`仅在延迟函数中有效。在正常的执行过程中，调用`recover`会返回`nil`，并且没有其它任何效果。如果当前的`goroutine`陷入恐慌，调用`recover`可以捕获到`panic`的输入值，并且恢复正常的执行。

下面这个函数演示了如何在过程中使用`panic` 

```go
var user = os.Getenv("USER")

func init() {
    if user == "" {
        panic("no value for $USER")
    }
}
```

下面这个函数检查作为其参数的函数在执行时是否会产生`panic`：

```go
func throwsPanic(f func()) (b bool) {
    defer func() {
        if x := recover(); x != nil {
            b = true
        }
    }()
    f() //执行函数f，如果f中出现了panic，那么就可以恢复回来
    return
}
```

## main 函数和 int 函数

Go里面有两个保留的函数：`init`函数（能够应用于所有的`package`）和`main`函数（只能应用于`package main`）。这两个函数在定义时不能有任何的参数和返回值。虽然一个`package`里面可以写任意多个`init`函数，但这无论是对于可读性还是以后的可维护性来说，我们都强烈建议用户在一个`package`中每个文件只写一个`init`函数。

Go程序会自动调用`init()`和`main()`，所以你不需要在任何地方调用这两个函数。每个`package`中的`init`函数都是可选的，但`package main`就必须包含一个`main`函数。

程序的初始化和执行都起始于`main`包。如果`main`包还导入了其它的包，那么就会在编译时将它们依次导入。有时一个包会被多个包同时导入，那么它只会被导入一次（例如很多包可能都会用到`fmt`包，但它只会被导入一次，因为没有必要导入多次）。当一个包被导入时，如果该包还导入了其它的包，那么会先将其它包导入进来，然后再对这些包中的包级常量和变量进行初始化，接着执行`init`函数（如果有的话），依次类推。等所有被导入的包都加载完毕了，就会开始对`main`包中的包级常量和变量进行初始化，然后执行`main`包中的`init`函数（如果存在的话），最后执行`main`函数。下图详细地解释了整个执行过程：

![](C:\Users\y5039\Pictures\Camera Roll\2.3.init.png)

​															图2.6 main函数引入包初始化流程图

## import

我们在写Go代码的时候经常用到import这个命令用来导入包文件，而我们经常看到的方式参考如下：

```go
import(
    "fmt"
)
```

然后我们代码里面可以通过如下的方式调用

```go
fmt.Println("hello world")
```

上面这个fmt是Go语言的标准库，其实是去`GOROOT`环境变量指定目录下去加载该模块，当然Go的import还支持如下两种方式来加载自己写的模块：

1. 相对路径

   import “./model” //当前文件同一目录的model目录，但是不建议这种方式来import

2. 绝对路径

   import “shorturl/model” //加载gopath/src/shorturl/model模块

上面展示了一些import常用的几种方式，但是还有一些特殊的import，让很多新手很费解，下面我们来一一讲解一下到底是怎么一回事

1.点操作

我们有时候会看到如下的方式导入包

```go
import(
      . "fmt"
  )
```

这个点操作的含义就是这个包导入之后在你调用这个包的函数时，你可以省略前缀的包名，也就是前面你调用的fmt.Println("hello world")可以省略的写成Println("hello world")

2.别名操作

别名操作顾名思义我们可以把包命名成另一个我们用起来容易记忆的名字

```go
import(
      f "fmt"
  )
```

别名操作的话调用包函数时前缀变成了我们的前缀，即f.Println("hello world")

3._ 操作

这个操作经常是让很多人费解的一个操作符，请看下面这个import

```go
import (
      "database/sql"
      _ "github.com/ziutek/mymysql/godrv"
  )
```

_ 操作其实是引入该包，而不直接使用包里面的函数，而是调用了该包里面的init函数。

# 2.4 struct类型

## struct

Go语言中，也和C或者其他语言一样，我们可以声明新的类型，作为其它类型的属性或字段的容器。例如，我们可以创建一个自定义类型`person`代表一个人的实体。这个实体拥有属性：姓名和年龄。这样的类型我们称之`struct`。如下代码所示:

```go
type person struct {
    name string
    age int
}
```

看到了吗？声明一个struct如此简单，上面的类型包含有两个字段

- 一个string类型的字段name，用来保存用户名称这个属性
- 一个int类型的字段age,用来保存用户年龄这个属性

如何使用struct呢？请看下面的代码

```go
type person struct {
    name string
    age int
}

var P person  // P现在就是person类型的变量了

P.name = "Astaxie"  // 赋值"Astaxie"给P的name属性.
P.age = 25  // 赋值"25"给变量P的age属性
fmt.Printf("The person's name is %s", P.name)  // 访问P的name属性.
```

除了上面这种P的声明使用之外，还有另外几种声明使用方式：

- 1.按照顺序提供初始化值

  P := person{"Tom", 25}

- 2.通过`field:value`的方式初始化，这样可以任意顺序

  P := person{age:24, name:"Tom"}

- 3.当然也可以通过`new`函数分配一个指针，此处P的类型为*person

  P := new(person)

下面我们看一个完整的使用struct的例子

```go
package main
import "fmt"

// 声明一个新的类型
type person struct {
    name string
    age int
}

// 比较两个人的年龄，返回年龄大的那个人，并且返回年龄差
// struct也是传值的
func Older(p1, p2 person) (person, int) {
    if p1.age>p2.age {  // 比较p1和p2这两个人的年龄
        return p1, p1.age-p2.age
    }
    return p2, p2.age-p1.age
}

func main() {
    var tom person

    // 赋值初始化
    tom.name, tom.age = "Tom", 18

    // 两个字段都写清楚的初始化
    bob := person{age:25, name:"Bob"}

    // 按照struct定义顺序初始化值
    paul := person{"Paul", 43}

    tb_Older, tb_diff := Older(tom, bob)
    tp_Older, tp_diff := Older(tom, paul)
    bp_Older, bp_diff := Older(bob, paul)

    fmt.Printf("Of %s and %s, %s is older by %d years\n",
        tom.name, bob.name, tb_Older.name, tb_diff)

    fmt.Printf("Of %s and %s, %s is older by %d years\n",
        tom.name, paul.name, tp_Older.name, tp_diff)

    fmt.Printf("Of %s and %s, %s is older by %d years\n",
        bob.name, paul.name, bp_Older.name, bp_diff)
}
```

## struct的匿名字段

我们上面介绍了如何定义一个struct，定义的时候是字段名与其类型一一对应，实际上Go支持只提供类型，而不写字段名的方式，也就是匿名字段，也称为嵌入字段。

当匿名字段是一个struct的时候，那么这个struct所拥有的全部字段都被隐式地引入了当前定义的这个struct。

让我们来看一个例子，让上面说的这些更具体化

```go
package main
import "fmt"

type Human struct {
    name string
    age int
    weight int
}

type Student struct {
    Human  // 匿名字段，那么默认Student就包含了Human的所有字段
    speciality string
}

func main() {
    // 我们初始化一个学生
    mark := Student{Human{"Mark", 25, 120}, "Computer Science"}

    // 我们访问相应的字段
    fmt.Println("His name is ", mark.name)
    fmt.Println("His age is ", mark.age)
    fmt.Println("His weight is ", mark.weight)
    fmt.Println("His speciality is ", mark.speciality)
    // 修改对应的备注信息
    mark.speciality = "AI"
    fmt.Println("Mark changed his speciality")
    fmt.Println("His speciality is ", mark.speciality)
    // 修改他的年龄信息
    fmt.Println("Mark become old")
    mark.age = 46
    fmt.Println("His age is", mark.age)
    // 修改他的体重信息
    fmt.Println("Mark is not an athlet anymore")
    mark.weight += 60
    fmt.Println("His weight is", mark.weight)
}
```

图例如下:

![](C:\Users\y5039\Pictures\Camera Roll\2.4.student_struct.png)

图2.7 Student和Human的方法继承

我们看到Student访问属性age和name的时候，就像访问自己所有用的字段一样，对，匿名字段就是这样，能够实现字段的继承。是不是很酷啊？还有比这个更酷的呢，那就是student还能访问Human这个字段作为字段名。请看下面的代码，是不是更酷了。

```go
mark.Human = Human{"Marcus", 55, 220}
mark.Human.age -= 1
```

通过匿名访问和修改字段相当的有用，但是不仅仅是struct字段哦，所有的内置类型和自定义类型都是可以作为匿名字段的。请看下面的例子

```go
package main
import "fmt"

type Skills []string

type Human struct {
    name string
    age int
    weight int
}

type Student struct {
    Human  // 匿名字段，struct
    Skills // 匿名字段，自定义的类型string slice
    int    // 内置类型作为匿名字段
    speciality string
}

func main() {
    // 初始化学生Jane
    jane := Student{Human:Human{"Jane", 35, 100}, speciality:"Biology"}
    // 现在我们来访问相应的字段
    fmt.Println("Her name is ", jane.name)
    fmt.Println("Her age is ", jane.age)
    fmt.Println("Her weight is ", jane.weight)
    fmt.Println("Her speciality is ", jane.speciality)
    // 我们来修改他的skill技能字段
    jane.Skills = []string{"anatomy"}
    fmt.Println("Her skills are ", jane.Skills)
    fmt.Println("She acquired two new ones ")
    jane.Skills = append(jane.Skills, "physics", "golang")
    fmt.Println("Her skills now are ", jane.Skills)
    // 修改匿名内置类型字段
    jane.int = 3
    fmt.Println("Her preferred number is", jane.int)
}
```

从上面例子我们看出来struct不仅仅能够将struct作为匿名字段、自定义类型、内置类型都可以作为匿名字段，而且可以在相应的字段上面进行函数操作（如例子中的append）。

这里有一个问题：如果human里面有一个字段叫做phone，而student也有一个字段叫做phone，那么该怎么办呢？

Go里面很简单的解决了这个问题，最外层的优先访问，也就是当你通过`student.phone`访问的时候，是访问student里面的字段，而不是human里面的字段。

这样就允许我们去重载通过匿名字段继承的一些字段，当然如果我们想访问重载后对应匿名类型里面的字段，可以通过匿名字段名来访问。请看下面的例子

```go
package main
import "fmt"

type Human struct {
    name string
    age int
    phone string  // Human类型拥有的字段
}

type Employee struct {
    Human  // 匿名字段Human
    speciality string
    phone string  // 雇员的phone字段
}

func main() {
    Bob := Employee{Human{"Bob", 34, "777-444-XXXX"}, "Designer", "333-222"}
    fmt.Println("Bob's work phone is:", Bob.phone)
    // 如果我们要访问Human的phone字段
    fmt.Println("Bob's personal phone is:", Bob.Human.phone)
}
```

# 2.5 面向对象

前面两章我们介绍了函数和struct，那你是否想过函数当作struct的字段一样来处理呢？今天我们就讲解一下函数的另一种形态，带有接收者的函数，我们称为`method`

## method

现在假设有这么一个场景，你定义了一个struct叫做长方形，你现在想要计算他的面积，那么按照我们一般的思路应该会用下面的方式来实现

```go
package main
import "fmt"

type Rectangle struct {
    width, height float64
}

func area(r Rectangle) float64 {
    return r.width*r.height
}

func main() {
    r1 := Rectangle{12, 2}
    r2 := Rectangle{9, 4}
    fmt.Println("Area of r1 is: ", area(r1))
    fmt.Println("Area of r2 is: ", area(r2))
}
```

这段代码可以计算出来长方形的面积，但是area()不是作为Rectangle的方法实现的（类似面向对象里面的方法），而是将Rectangle的对象（如r1,r2）作为参数传入函数计算面积的。

这样实现当然没有问题咯，但是当需要增加圆形、正方形、五边形甚至其它多边形的时候，你想计算他们的面积的时候怎么办啊？那就只能增加新的函数咯，但是函数名你就必须要跟着换了，变成`area_rectangle, area_circle, area_triangle...`

像下图所表示的那样， 椭圆代表函数, 而这些函数并不从属于struct(或者以面向对象的术语来说，并不属于class)，他们是单独存在于struct外围，而非在概念上属于某个struct的。

![](C:\Users\y5039\Pictures\Camera Roll\2.5.rect_func_without_receiver.png)

​																				图2.8 方法和struct的关系图

很显然，这样的实现并不优雅，并且从概念上来说"面积"是"形状"的一个属性，它是属于这个特定的形状的，就像长方形的长和宽一样。

基于上面的原因所以就有了`method`的概念，`method`是附属在一个给定的类型上的，他的语法和函数的声明语法几乎一样，只是在`func`后面增加了一个receiver(也就是method所依从的主体)。

用上面提到的形状的例子来说，method `area()` 是依赖于某个形状(比如说Rectangle)来发生作用的。Rectangle.area()的发出者是Rectangle， area()是属于Rectangle的方法，而非一个外围函数。

更具体地说，Rectangle存在字段length 和 width, 同时存在方法area(), 这些字段和方法都属于Rectangle。

用Rob Pike的话来说就是：

> **"A method is a function with an implicit first argument, called a receiver."**

method的语法如下：

```go
func (r ReceiverType) funcName(parameters) (results)
```

下面我们把最开始的例子用method来实现：

```go
package main
import (
    "fmt"
    "math"
)

type Rectangle struct {
    width, height float64
}

type Circle struct {
    radius float64
}

func (r Rectangle) area() float64 {
    return r.width*r.height
}

func (c Circle) area() float64 {
    return c.radius * c.radius * math.Pi
}

func main() {
    r1 := Rectangle{12, 2}
    r2 := Rectangle{9, 4}
    c1 := Circle{10}
    c2 := Circle{25}

    fmt.Println("Area of r1 is: ", r1.area())
    fmt.Println("Area of r2 is: ", r2.area())
    fmt.Println("Area of c1 is: ", c1.area())
    fmt.Println("Area of c2 is: ", c2.area())
}
```

在使用method的时候重要注意几点

- 虽然method的名字一模一样，但是如果接收者不一样，那么method就不一样
- method里面可以访问接收者的字段
- 调用method通过`.`访问，就像struct里面访问字段一样

图示如下:

![](C:\Users\y5039\Pictures\Camera Roll\2.5.shapes_func_with_receiver_cp.png)

图2.9 不同struct的method不同

在上例，method area() 分别属于Rectangle和Circle， 于是他们的 Receiver 就变成了Rectangle 和 Circle, 或者说，这个area()方法 是由 Rectangle/Circle 发出的。

> 值得说明的一点是，图示中method用虚线标出，意思是此处方法的Receiver是以值传递，而非引用传递，是的，Receiver还可以是指针, 两者的差别在于, 指针作为Receiver会对实例对象的内容发生操作,而普通类型作为Receiver仅仅是以副本作为操作对象,并不对原实例对象发生操作。后文对此会有详细论述。

那是不是method只能作用在struct上面呢？当然不是咯，他可以定义在任何你自定义的类型、内置类型、struct等各种类型上面。这里你是不是有点迷糊了，什么叫自定义类型，自定义类型不就是struct嘛，不是这样的哦，struct只是自定义类型里面一种比较特殊的类型而已，还有其他自定义类型申明，可以通过如下这样的申明来实现。

```go
type typeName typeLiteral
```

请看下面这个申明自定义类型的代码

```go
type ages int

type money float32

type months map[string]int

m := months {
    "January":31,
    "February":28,
    ...
    "December":31,
}
```

看到了吗？简单的很吧，这样你就可以在自己的代码里面定义有意义的类型了，实际上只是一个定义了一个别名,有点类似于c中的typedef，例如上面ages替代了int

好了，让我们回到`method`

你可以在任何的自定义类型中定义任意多的`method`，接下来让我们看一个复杂一点的例子：

```go
package main
import "fmt"

const(
    WHITE = iota
    BLACK
    BLUE
    RED
    YELLOW
)

type Color byte

type Box struct {
    width, height, depth float64
    color Color
}

type BoxList []Box //a slice of boxes

func (b Box) Volume() float64 {
    return b.width * b.height * b.depth
}

func (b *Box) SetColor(c Color) {
    b.color = c
}

func (bl BoxList) BiggestColor() Color {
    v := 0.00
    k := Color(WHITE)
    for _, b := range bl {
        if bv := b.Volume(); bv > v {
            v = bv
            k = b.color
        }
    }
    return k
}

func (bl BoxList) PaintItBlack() {
    for i, _ := range bl {
        bl[i].SetColor(BLACK)
    }
}

func (c Color) String() string {
    strings := []string {"WHITE", "BLACK", "BLUE", "RED", "YELLOW"}
    return strings[c]
}

func main() {
    boxes := BoxList {
        Box{4, 4, 4, RED},
        Box{10, 10, 1, YELLOW},
        Box{1, 1, 20, BLACK},
        Box{10, 10, 1, BLUE},
        Box{10, 30, 1, WHITE},
        Box{20, 20, 20, YELLOW},
    }

    fmt.Printf("We have %d boxes in our set\n", len(boxes))
    fmt.Println("The volume of the first one is", boxes[0].Volume(), "cm³")
    fmt.Println("The color of the last one is",boxes[len(boxes)-1].color.String())
    fmt.Println("The biggest one is", boxes.BiggestColor().String())

    fmt.Println("Let's paint them all black")
    boxes.PaintItBlack()
    fmt.Println("The color of the second one is", boxes[1].color.String())

    fmt.Println("Obviously, now, the biggest one is", boxes.BiggestColor().String())
}
```

上面的代码通过const定义了一些常量，然后定义了一些自定义类型

- Color作为byte的别名
- 定义了一个struct:Box，含有三个长宽高字段和一个颜色属性
- 定义了一个slice:BoxList，含有Box

然后以上面的自定义类型为接收者定义了一些method

- Volume()定义了接收者为Box，返回Box的容量
- SetColor(c Color)，把Box的颜色改为c
- BiggestColor()定在在BoxList上面，返回list里面容量最大的颜色
- PaintItBlack()把BoxList里面所有Box的颜色全部变成黑色
- String()定义在Color上面，返回Color的具体颜色(字符串格式)

上面的代码通过文字描述出来之后是不是很简单？我们一般解决问题都是通过问题的描述，去写相应的代码实现。

## 指针作为receiver

现在让我们回过头来看看SetColor这个method，它的receiver是一个指向Box的指针，是的，你可以使用*Box。想想为啥要使用指针而不是Box本身呢？

我们定义SetColor的真正目的是想改变这个Box的颜色，如果不传Box的指针，那么SetColor接受的其实是Box的一个copy，也就是说method内对于颜色值的修改，其实只作用于Box的copy，而不是真正的Box。所以我们需要传入指针。

这里可以把receiver当作method的第一个参数来看，然后结合前面函数讲解的传值和传引用就不难理解

这里你也许会问了那SetColor函数里面应该这样定义`*b.Color=c`,而不是`b.Color=c`,因为我们需要读取到指针相应的值。

你是对的，其实Go里面这两种方式都是正确的，当你用指针去访问相应的字段时(虽然指针没有任何的字段)，Go知道你要通过指针去获取这个值，看到了吧，Go的设计是不是越来越吸引你了。

也许细心的读者会问这样的问题，PaintItBlack里面调用SetColor的时候是不是应该写成`(&bl[i]).SetColor(BLACK)`，因为SetColor的receiver是*Box，而不是Box。

你又说对的，这两种方式都可以，因为Go知道receiver是指针，他自动帮你转了。

也就是说：

> 如果一个method的receiver是*T,你可以在一个T类型的实例变量V上面调用这个method，而不需要&V去调用这个method

类似的

> 如果一个method的receiver是T，你可以在一个*T类型的变量P上面调用这个method，而不需要* P去调用这个method

所以，你不用担心你是调用的指针的method还是不是指针的method，Go知道你要做的一切，这对于有多年C/C++编程经验的同学来说，真是解决了一个很大的痛苦。

## method继承

前面一章我们学习了字段的继承，那么你也会发现Go的一个神奇之处，method也是可以继承的。如果匿名字段实现了一个method，那么包含这个匿名字段的struct也能调用该method。让我们来看下面这个例子

```go
package main
import "fmt"

type Human struct {
    name string
    age int
    phone string
}

type Student struct {
    Human //匿名字段
    school string
}

type Employee struct {
    Human //匿名字段
    company string
}

//在human上面定义了一个method
func (h *Human) SayHi() {
    fmt.Printf("Hi, I am %s you can call me on %s\n", h.name, h.phone)
}

func main() {
    mark := Student{Human{"Mark", 25, "222-222-YYYY"}, "MIT"}
    sam := Employee{Human{"Sam", 45, "111-888-XXXX"}, "Golang Inc"}

    mark.SayHi()
    sam.SayHi()
}
```

### method重写

上面的例子中，如果Employee想要实现自己的SayHi,怎么办？简单，和匿名字段冲突一样的道理，我们可以在Employee上面定义一个method，重写了匿名字段的方法。请看下面的例子

```go
package main
import "fmt"

type Human struct {
    name string
    age int
    phone string
}

type Student struct {
    Human //匿名字段
    school string
}

type Employee struct {
    Human //匿名字段
    company string
}

//Human定义method
func (h *Human) SayHi() {
    fmt.Printf("Hi, I am %s you can call me on %s\n", h.name, h.phone)
}

//Employee的method重写Human的method
func (e *Employee) SayHi() {
    fmt.Printf("Hi, I am %s, I work at %s. Call me on %s\n", e.name,
        e.company, e.phone) //Yes you can split into 2 lines here.
}

func main() {
    mark := Student{Human{"Mark", 25, "222-222-YYYY"}, "MIT"}
    sam := Employee{Human{"Sam", 45, "111-888-XXXX"}, "Golang Inc"}

    mark.SayHi()
    sam.SayHi()
}
```

上面的代码设计的是如此的美妙，让人不自觉的为Go的设计惊叹！

通过这些内容，我们可以设计出基本的面向对象的程序了，但是Go里面的面向对象是如此的简单，没有任何的私有、公有关键字，通过大小写来实现(大写开头的为公有，小写开头的为私有)，方法也同样适用这个原则。

# 2.6 interface

## interface

Go语言里面设计最精妙的应该算interface，它让面向对象，内容组织实现非常的方便，当你看完这一章，你就会被interface的巧妙设计所折服。 

## 什么是interface

简单的说，interface是一组method的组合，我们通过interface来定义对象的一组行为。

我们前面一章最后一个例子中Student和Employee都能SayHi，虽然他们的内部实现不一样，但是那不重要，重要的是他们都能`say hi`

让我们来继续做更多的扩展，Student和Employee实现另一个方法`Sing`，然后Student实现方法BorrowMoney而Employee实现SpendSalary。

这样Student实现了三个方法：SayHi、Sing、BorrowMoney；而Employee实现了SayHi、Sing、SpendSalary。

上面这些方法的组合称为interface(被对象Student和Employee实现)。例如Student和Employee都实现了interface：SayHi和Sing，也就是这两个对象是该interface类型。而Employee没有实现这个interface：SayHi、Sing和BorrowMoney，因为Employee没有实现BorrowMoney这个方法。

## interface类型

interface类型定义了一组方法，如果某个对象实现了某个接口的所有方法，则此对象就实现了此接口。详细的语法参考下面这个例子:

```go
type Human struct {
    name string
    age int
    phone string
}

type Student struct {
    Human //匿名字段Human
    school string
    loan float32
}

type Employee struct {
    Human //匿名字段Human
    company string
    money float32
}

//Human对象实现Sayhi方法
func (h *Human) SayHi() {
    fmt.Printf("Hi, I am %s you can call me on %s\n", h.name, h.phone)
}

// Human对象实现Sing方法
func (h *Human) Sing(lyrics string) {
    fmt.Println("La la, la la la, la la la la la...", lyrics)
}
//Human对象实现Guzzle方法
func (h *Human) Guzzle(beerStein string) {
    fmt.Println("Guzzle Guzzle Guzzle...", beerStein)
}

// Employee重载Human的Sayhi方法
func (e *Employee) SayHi() {
    fmt.Printf("Hi, I am %s, I work at %s. Call me on %s\n", e.name,
        e.company, e.phone) //此句可以分成多行
}

//Student实现BorrowMoney方法
func (s *Student) BorrowMoney(amount float32) {
    s.loan += amount // (again and again and...)
}

//Employee实现SpendSalary方法
func (e *Employee) SpendSalary(amount float32) {
    e.money -= amount // More vodka please!!! Get me through the day!
}

// 定义interface
type Men interface {
    SayHi()
    Sing(lyrics string)
    Guzzle(beerStein string)
}

type YoungChap interface {
    SayHi()
    Sing(song string)
    BorrowMoney(amount float32)
}

type ElderlyGent interface {
    SayHi()
    Sing(song string)
    SpendSalary(amount float32)
}
```

通过上面的代码我们可以知道，interface可以被任意的对象实现。我们看到上面的Men interface被Human、Student和Employee实现。同理，一个对象可以实现任意多个interface，例如上面的Student实现了Men和YoungChap两个interface。

最后，任意的类型都实现了空interface(我们这样定义：interface{})，也就是包含0个method的interface。

## interface值

那么interface里面到底能存什么值呢？如果我们定义了一个interface的变量，那么这个变量里面可以存实现这个interface的任意类型的对象。例如上面例子中，我们定义了一个Men interface类型的变量m，那么m里面可以存Human、Student或者Employee值。

因为m能够持有这三种类型的对象，所以我们可以定义一个包含Men类型元素的slice，这个slice可以被赋予实现了Men接口的任意结构的对象，这个和我们传统意义上面的slice有所不同。

让我们来看一下下面这个例子:

```go
package main
import "fmt"

type Human struct {
    name string
    age int
    phone string
}

type Student struct {
    Human //匿名字段
    school string
    loan float32
}

type Employee struct {
    Human //匿名字段
    company string
    money float32
}

//Human实现SayHi方法
func (h Human) SayHi() {
    fmt.Printf("Hi, I am %s you can call me on %s\n", h.name, h.phone)
}

//Human实现Sing方法
func (h Human) Sing(lyrics string) {
    fmt.Println("La la la la...", lyrics)
}

//Employee重载Human的SayHi方法
func (e Employee) SayHi() {
    fmt.Printf("Hi, I am %s, I work at %s. Call me on %s\n", e.name,
        e.company, e.phone)
    }

// Interface Men被Human,Student和Employee实现
// 因为这三个类型都实现了这两个方法
type Men interface {
    SayHi()
    Sing(lyrics string)
}

func main() {
    mike := Student{Human{"Mike", 25, "222-222-XXX"}, "MIT", 0.00}
    paul := Student{Human{"Paul", 26, "111-222-XXX"}, "Harvard", 100}
    sam := Employee{Human{"Sam", 36, "444-222-XXX"}, "Golang Inc.", 1000}
    tom := Employee{Human{"Tom", 37, "222-444-XXX"}, "Things Ltd.", 5000}

    //定义Men类型的变量i
    var i Men

    //i能存储Student
    i = mike
    fmt.Println("This is Mike, a Student:")
    i.SayHi()
    i.Sing("November rain")

    //i也能存储Employee
    i = tom
    fmt.Println("This is tom, an Employee:")
    i.SayHi()
    i.Sing("Born to be wild")

    //定义了slice Men
    fmt.Println("Let's use a slice of Men and see what happens")
    x := make([]Men, 3)
    //这三个都是不同类型的元素，但是他们实现了interface同一个接口
    x[0], x[1], x[2] = paul, sam, mike

    for _, value := range x{
        value.SayHi()
    }
}
```

通过上面的代码，你会发现interface就是一组抽象方法的集合，它必须由其他非interface类型实现，而不能自我实现， Go通过interface实现了duck-typing:即"当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子"。

## 空interface

空interface(interface{})不包含任何的method，正因为如此，所有的类型都实现了空interface。空interface对于描述起不到任何的作用(因为它不包含任何的method），但是空interface在我们需要存储任意类型的数值的时候相当有用，因为它可以存储任意类型的数值。它有点类似于C语言的void*类型。

```go
// 定义a为空接口
var a interface{}
var i int = 5
s := "Hello world"
// a可以存储任意类型的数值
a = i
a = s
```

一个函数把interface{}作为参数，那么他可以接受任意类型的值作为参数，如果一个函数返回interface{},那么也就可以返回任意类型的值。是不是很有用啊！

## interface函数参数

interface的变量可以持有任意实现该interface类型的对象，这给我们编写函数(包括method)提供了一些额外的思考，我们是不是可以通过定义interface参数，让函数接受各种类型的参数。

举个例子：fmt.Println是我们常用的一个函数，但是你是否注意到它可以接受任意类型的数据。打开fmt的源码文件，你会看到这样一个定义:

```go
type Stringer interface {
     String() string
}
```

也就是说，任何实现了String方法的类型都能作为参数被fmt.Println调用,让我们来试一试:

```go
package main
import (
    "fmt"
    "strconv"
)

type Human struct {
    name string
    age int
    phone string
}

// 通过这个方法 Human 实现了 fmt.Stringer
func (h Human) String() string {
    return "❰"+h.name+" - "+strconv.Itoa(h.age)+" years -  ✆ " +h.phone+"❱"
}

func main() {
    Bob := Human{"Bob", 39, "000-7777-XXX"}
    fmt.Println("This Human is : ", Bob)
}
```

现在我们再回顾一下前面的Box示例，你会发现Color结构也定义了一个method：String。其实这也是实现了fmt.Stringer这个interface，即如果需要某个类型能被fmt包以特殊的格式输出，你就必须实现Stringer这个接口。如果没有实现这个接口，fmt将以默认的方式输出。

```go
//实现同样的功能
fmt.Println("The biggest one is", boxes.BiggestsColor().String())
fmt.Println("The biggest one is", boxes.BiggestsColor())
```

注：实现了error接口的对象（即实现了Error() string的对象），使用fmt输出时，会调用Error()方法，因此不必再定义String()方法了。

## interface变量存储的类型

我们知道interface的变量里面可以存储任意类型的数值(该类型实现了interface)。那么我们怎么反向知道这个变量里面实际保存了的是哪个类型的对象呢？目前常用的有两种方法：

- Comma-ok断言

  Go语言里面有一个语法，可以直接判断是否是该类型的变量： value, ok = element.(T)，这里value就是变量的值，ok是一个bool类型，element是interface变量，T是断言的类型。

  如果element里面确实存储了T类型的数值，那么ok返回true，否则返回false。

  让我们通过一个例子来更加深入的理解。

  ```go
  package main
  
    import (
        "fmt"
        "strconv"
    )
  
    type Element interface{}
    type List [] Element
  
    type Person struct {
        name string
        age int
    }
  
    //定义了String方法，实现了fmt.Stringer
    func (p Person) String() string {
        return "(name: " + p.name + " - age: "+strconv.Itoa(p.age)+ " years)"
    }
  
    func main() {
        list := make(List, 3)
        list[0] = 1 // an int
        list[1] = "Hello" // a string
        list[2] = Person{"Dennis", 70}
  
        for index, element := range list {
            if value, ok := element.(int); ok {
                fmt.Printf("list[%d] is an int and its value is %d\n", index, value)
            } else if value, ok := element.(string); ok {
                fmt.Printf("list[%d] is a string and its value is %s\n", index, value)
            } else if value, ok := element.(Person); ok {
                fmt.Printf("list[%d] is a Person and its value is %s\n", index, value)
            } else {
                fmt.Printf("list[%d] is of a different type\n", index)
            }
        }
    }
  ```

  

是不是很简单啊，同时你是否注意到了多个if里面，还记得我前面介绍流程时讲过，if里面允许初始化变量。

也许你注意到了，我们断言的类型越多，那么if else也就越多，所以才引出了下面要介绍的switch。

- switch测试

最好的讲解就是代码例子，现在让我们重写上面的这个实现

```go
package main

  import (
      "fmt"
      "strconv"
  )

  type Element interface{}
  type List [] Element

  type Person struct {
      name string
      age int
  }

  //打印
  func (p Person) String() string {
      return "(name: " + p.name + " - age: "+strconv.Itoa(p.age)+ " years)"
  }

  func main() {
      list := make(List, 3)
      list[0] = 1 //an int
      list[1] = "Hello" //a string
      list[2] = Person{"Dennis", 70}

      for index, element := range list{
          switch value := element.(type) {
              case int:
                  fmt.Printf("list[%d] is an int and its value is %d\n", index, value)
              case string:
                  fmt.Printf("list[%d] is a string and its value is %s\n", index, value)
              case Person:
                  fmt.Printf("list[%d] is a Person and its value is %s\n", index, value)
              default:
                  fmt.Println("list[%d] is of a different type", index)
          }
      }
  }
```

这里有一点需要强调的是：`element.(type)`语法不能在switch外的任何逻辑里面使用，如果你要在switch外面判断一个类型就使用`comma-ok`。

## 嵌入interface

Go里面真正吸引人的是它内置的逻辑语法，就像我们在学习Struct时学习的匿名字段，多么的优雅啊，那么相同的逻辑引入到interface里面，那不是更加完美了。如果一个interface1作为interface2的一个嵌入字段，那么interface2隐式的包含了interface1里面的method。

我们可以看到源码包container/heap里面有这样的一个定义

```go
type Interface interface {
    sort.Interface //嵌入字段sort.Interface
    Push(x interface{}) //a Push method to push elements into the heap
    Pop() interface{} //a Pop elements that pops elements from the heap
}
```

我们看到sort.Interface其实就是嵌入字段，把sort.Interface的所有method给隐式的包含进来了。也就是下面三个方法：

```go
type Interface interface {
    // Len is the number of elements in the collection.
    Len() int
    // Less returns whether the element with index i should sort
    // before the element with index j.
    Less(i, j int) bool
    // Swap swaps the elements with indexes i and j.
    Swap(i, j int)
}
```

另一个例子就是io包下面的 io.ReadWriter ，它包含了io包下面的Reader和Writer两个interface：

```go
// io.ReadWriter
type ReadWriter interface {
    Reader
    Writer
}
```

## 反射

Go语言实现了反射，所谓反射就是能检查程序在运行时的状态。我们一般用到的包是reflect包。如何运用reflect包，官方的这篇文章详细的讲解了reflect包的实现原理，[laws of reflection](http://golang.org/doc/articles/laws_of_reflection.html)

使用reflect一般分成三步，下面简要的讲解一下：要去反射一个类型的值(这些值都实现了空interface)，首先需要把它转化成reflect对象(reflect.Type或者reflect.Value，根据不同的情况调用不同的函数)。这两种获取方式如下：

```go
t := reflect.TypeOf(i)    //得到类型的元数据,通过t我们能获取类型定义里面的所有元素
v := reflect.ValueOf(i)   //得到实际的值，通过v我们获取存储在里面的值，还可以去改变值
```

转化为reflect对象之后我们就可以进行一些操作了，也就是将reflect对象转化成相应的值，例如

```go
tag := t.Elem().Field(0).Tag  //获取定义在struct里面的标签
name := v.Elem().Field(0).String()  //获取存储在第一个字段里面的值
```

获取反射值能返回相应的类型和数值

```go
var x float64 = 3.4
v := reflect.ValueOf(x)
fmt.Println("type:", v.Type())
fmt.Println("kind is float64:", v.Kind() == reflect.Float64)
fmt.Println("value:", v.Float())
```

最后，反射的话，那么反射的字段必须是可修改的，我们前面学习过传值和传引用，这个里面也是一样的道理。反射的字段必须是可读写的意思是，如果下面这样写，那么会发生错误

```go
var x float64 = 3.4
v := reflect.ValueOf(x)
v.SetFloat(7.1)
```

如果要修改相应的值，必须这样写:

```go
var x float64 = 3.4
p := reflect.ValueOf(&x)
v := p.Elem()
v.SetFloat(7.1)
```

上面只是对反射的简单介绍，更深入的理解还需要自己在编程中不断的实践。

# 2.7 并发

有人把Go比作21世纪的C语言，第一是因为Go语言设计简单，第二，21世纪最重要的就是并行程序设计，而Go从语言层面就支持了并行。

## goroutine

goroutine是Go并行设计的核心。goroutine说到底其实就是线程，但是它比线程更小，十几个goroutine可能体现在底层就是五六个线程，Go语言内部帮你实现了这些goroutine之间的内存共享。执行goroutine只需极少的栈内存(大概是4~5KB)，当然会根据相应的数据伸缩。也正因为如此，可同时运行成千上万个并发任务。goroutine比thread更易用、更高效、更轻便。

goroutine是通过Go的runtime管理的一个线程管理器。goroutine通过`go`关键字实现了，其实就是一个普通的函数。

```go
go hello(a, b, c)
```



通过关键字go就启动了一个goroutine。我们来看一个例子

```go
package main

import (
    "fmt"
    "runtime"
)

func say(s string) {
    for i := 0; i < 5; i++ {
        runtime.Gosched()
        fmt.Println(s)
    }
}

func main() {
    go say("world") //开一个新的Goroutines执行
    say("hello") //当前Goroutines执行
}

// 以上程序执行后将输出：
// hello
// world
// hello
// world
// hello
// world
// hello
// world
// hello
```

我们可以看到go关键字很方便的就实现了并发编程。 上面的多个goroutine运行在同一个进程里面，共享内存数据，不过设计上我们要遵循：不要通过共享来通信，而要通过通信来共享。

> runtime.Gosched()表示让CPU把时间片让给别人,下次某个时候继续恢复执行该goroutine。
>
> 默认情况下，调度器仅使用单线程，也就是说只实现了并发。想要发挥多核处理器的并行，需要在我们的程序中显式调用 runtime.GOMAXPROCS(n) 告诉调度器同时使用多个线程。GOMAXPROCS 设置了同时运行逻辑代码的系统线程的最大数量，并返回之前的设置。如果n < 1，不会改变当前设置。以后Go的新版本中调度得到改进后，这将被移除。这里有一篇Rob介绍的关于并发和并行的文章：<http://concur.rspace.googlecode.com/hg/talk/concur.html#landing-slide>

## channels

goroutine运行在相同的地址空间，因此访问共享内存必须做好同步。那么goroutine之间如何进行数据的通信呢，Go提供了一个很好的通信机制channel。channel可以与Unix shell 中的双向管道做类比：可以通过它发送或者接收值。这些值只能是特定的类型：channel类型。定义一个channel时，也需要定义发送到channel的值的类型。注意，必须使用make 创建channel：

```go
ci := make(chan int)
cs := make(chan string)
cf := make(chan interface{})
```

channel通过操作符`<-`来接收和发送数据

```go
ch <- v    // 发送v到channel ch.
v := <-ch  // 从ch中接收数据，并赋值给v
```

我们把这些应用到我们的例子中来：

```go
package main

import "fmt"

func sum(a []int, c chan int) {
    total := 0
    for _, v := range a {
        total += v
    }
    c <- total  // send total to c
}

func main() {
    a := []int{7, 2, 8, -9, 4, 0}

    c := make(chan int)
    go sum(a[:len(a)/2], c)
    go sum(a[len(a)/2:], c)
    x, y := <-c, <-c  // receive from c

    fmt.Println(x, y, x + y)
}
```

默认情况下，channel接收和发送数据都是阻塞的，除非另一端已经准备好，这样就使得Goroutines同步变的更加的简单，而不需要显式的lock。所谓阻塞，也就是如果读取（value := <-ch）它将会被阻塞，直到有数据接收。其次，任何发送（ch<-5）将会被阻塞，直到数据被读出。无缓冲channel是在多个goroutine之间同步很棒的工具。

## Buffered Channels

上面我们介绍了默认的非缓存类型的channel，不过Go也允许指定channel的缓冲大小，很简单，就是channel可以存储多少元素。ch:= make(chan bool, 4)，创建了可以存储4个元素的bool 型channel。在这个channel 中，前4个元素可以无阻塞的写入。当写入第5个元素时，代码将会阻塞，直到其他goroutine从channel 中读取一些元素，腾出空间。

```go
ch := make(chan type, value)

value == 0 ! 无缓冲（阻塞）
value > 0 ! 缓冲（非阻塞，直到value 个元素）
```

我们看一下下面这个例子，你可以在自己本机测试一下，修改相应的value值

```go
package main

import "fmt"

func main() {
    c := make(chan int, 2)//修改2为1就报错，修改2为3可以正常运行
    c <- 1
    c <- 2
    fmt.Println(<-c)
    fmt.Println(<-c)
}
    //修改为1报如下的错误:
    //fatal error: all goroutines are asleep - deadlock!
```

## Range和Close

上面这个例子中，我们需要读取两次c，这样不是很方便，Go考虑到了这一点，所以也可以通过range，像操作slice或者map一样操作缓存类型的channel，请看下面的例子

```go
package main

import (
    "fmt"
)

func fibonacci(n int, c chan int) {
    x, y := 1, 1
    for i := 0; i < n; i++ {
        c <- x
        x, y = y, x + y
    }
    close(c)
}

func main() {
    c := make(chan int, 10)
    go fibonacci(cap(c), c)
    for i := range c {
        fmt.Println(i)
    }
}
```

`for i := range c`能够不断的读取channel里面的数据，直到该channel被显式的关闭。上面代码我们看到可以显式的关闭channel，生产者通过内置函数`close`关闭channel。关闭channel之后就无法再发送任何数据了，在消费方可以通过语法`v, ok := <-ch`测试channel是否被关闭。如果ok返回false，那么说明channel已经没有任何数据并且已经被关闭。

> 记住应该在生产者的地方关闭channel，而不是消费的地方去关闭它，这样容易引起panic
>
> 另外记住一点的就是channel不像文件之类的，不需要经常去关闭，只有当你确实没有任何发送数据了，或者你想显式的结束range循环之类的

## Select

我们上面介绍的都是只有一个channel的情况，那么如果存在多个channel的时候，我们该如何操作呢，Go里面提供了一个关键字`select`，通过`select`可以监听channel上的数据流动。

`select`默认是阻塞的，只有当监听的channel中有发送或接收可以进行时才会运行，当多个channel都准备好的时候，select是随机的选择一个执行的。

```go
package main

import "fmt"

func fibonacci(c, quit chan int) {
    x, y := 1, 1
    for {
        select {
        case c <- x:
            x, y = y, x + y
        case <-quit:
            fmt.Println("quit")
            return
        }
    }
}

func main() {
    c := make(chan int)
    quit := make(chan int)
    go func() {
        for i := 0; i < 10; i++ {
            fmt.Println(<-c)
        }
        quit <- 0
    }()
    fibonacci(c, quit)
}
```

在`select`里面还有default语法，`select`其实就是类似switch的功能，default就是当监听的channel都没有准备好的时候，默认执行的（select不再阻塞等待channel）。

```go
select {
case i := <-c:
    // use i
default:
    // 当c阻塞的时候执行这里
}
```

## 超时

有时候会出现goroutine阻塞的情况，那么我们如何避免整个程序进入阻塞的情况呢？我们可以利用select来设置超时，通过如下的方式实现：

```go
func main() {
    c := make(chan int)
    o := make(chan bool)
    go func() {
        for {
            select {
                case v := <- c:
                    println(v)
                case <- time.After(5 * time.Second):
                    println("timeout")
                    o <- true
                    break
            }
        }
    }()
    <- o
}
```

## runtime goroutine

runtime包中有几个处理goroutine的函数：

- Goexit

  退出当前执行的goroutine，但是defer函数还会继续调用

- Gosched

  让出当前goroutine的执行权限，调度器安排其他等待的任务运行，并在下次某个时候从该位置恢复执行。

- NumCPU

  返回 CPU 核数量

- NumGoroutine

  返回正在执行和排队的任务总数

- GOMAXPROCS

  用来设置可以并行计算的CPU核数的最大值，并返回之前的值。
  
  

武汉-猪(1728565484)  1:11:30 PM
调用函数，就是 public functionName
可以直接使用，所以是  pakageName.FunctionName
方法是绑定在结构体里，调用的前提是，存在这个结构体实例
所以方法调用方法是， packageName.Object{}.MethodName