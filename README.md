# DailySwift
开一个swift的坑更新学习进度。

前期以学语法为主，中后期代码跟进。

报了一个rxSwift的班，之后将探索它在项目中的实际使用。

update:在开始的时候，我觉得记录这些进度很有用。然而我发现自己并不能比文档翻译做的更好，总是在复制和粘贴(也很感谢MWeb这个工具，让我偷懒不少)。

------
## Day1 2016/08/10
根据 [Swift 学习指引](http://www.swiftguide.cn/)中推荐的资料开始学习。

我选择的是[梁杰numbbbbb](https://github.com/numbbbbb/)组织翻译的[The Swift Programing Language 中文版](https://github.com/numbbbbb/the-swift-programming-language-in-chinese)，目前更新到的是swift2.2。挂在极客学院的wiki：
>http://wiki.jikexueyuan.com/project/swift/

非常感谢这么一群人的贡献。

学好英语是多么重要，直接上原版 : ]

## swift代码规范
学习阅读swift的一点基本代码规范。

经过近两年的编程学习，从懵懂无知，到稍有所悟，也明白了代码规范的重要性。

Google了一下，发现这一篇[swift编码规范](http://www.cocoachina.com/swift/20141105/10145.html)，翻译自raywenderlich的[swift编程风格指南](https://github.com/raywenderlich/swift-style-guide)。

打算按照这个风格进行编码。

## Playground
下载官方的 Playground 并双击文件在 Xcode 里打开，地址如下:
>https://developer.apple.com/go/?id=swift-tour

根据这一份playground做一个快速入门。

## 基础部分
### let 和 var
swift里:

let表示常量，即它的值是不可变的;
var表示变量，即它的值为可变。

在声明常量和变量时，可以添加类型标注(type annotation)。

但是要注意，在常量名和变量名后面，加一个冒号和空格

正确的写法：

 	var welcomeMessage: String

错误的写法：

 	var welcomeMessage:String


可以在一行中，声明多个变量:

	var red, green, blue: Double

值得一提的是，在swift中，你可以用任何你喜欢的字符来给常量和变量命名，包括Unicode字符：

	let π = 3.14159
	let 你好 = "你好世界"
	let 🐶🐮 = "dogcow"
	

### print输出

和C语言一样，我们可以用print来输出常量和变量。

	var friendlyWelcome = "Hello!"
	friendlyWelcome = "Bonjour!"
	print("The current value of friendlyWelcome is \(friendlyWelcome)")

输出 ：
>"The current value of friendlyWelcome is Bonjour!"

### 类型安全
swift是一个类型安全（type safe）的语言。

它会在编译你的代码时，进行类型检查（type checks），并把不匹配的类型标记为错误。

可选（Optional）类型就是一个很好的例子:

可选类型用于处理值缺失的情况。可选，表示“那儿有一个值，并且它等于 x ”或者“那儿没有值”。

可选有点像在 Objective-C 中使用nil，但是它可以用在任何类型上，不仅仅是类。

>可选类型比 Objective-C 中的nil指针更加安全,也更具表现力，它是 Swift 许多强大特性的重要组成部分。

Swift 可以让你清楚地知道值的类型。如果你的代码期望得到一个`String`，类型安全会阻止你不小心传入一个`Int`。你可以在开发阶段尽早发现并修正错误。

### 类型检查

处理不同类型的值时，类型检查可以帮你避免错误。

当你在声明常量或者变量的时候,赋给它们一个字面量（literal value 或 literal）即可触发类型推断。

>推断浮点数的类型时，Swift 总是会选择`Double`而不是`Float`。

如果表达式中同时出现了整数和浮点数，会被推断为`Double`类型：

```
let anotherPi = 3 + 0.14159
// anotherPi 会被推测为 Double 类型
```

原因在于，原始值`3`没有显式声明类型，而表达式中出现了一个浮点字面量，所以表达式会被推断为`Double`类型。

### 整数和浮点数转换
整数和浮点数的转换必须显式指定类型：

```
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi 等于 3.14159，所以被推测为 Double 类型
```

这个例子中，常量`three`的值被用来创建一个`Double`类型的值，所以加号`两边的数类型须相同`。

如果不进行转换，两者无法相加。

浮点数到整数的反向转换同样行，整数类型可以用`Double`或者`Float`类型来初始化：

```
let integerPi = Int(pi)
// integerPi 等于 3，所以被推测为 Int 类型
```

当用这种方式来初始化一个新的整数值时，浮点值会被截断。也就是说`4.75`会变成`4`，`-3.9`会变成`-3`。

> 注意：
> 结合数字类常量和变量不同于结合数字类字面量。字面量`3`可以直接和字面量`0.14159`相加，因为数字字面量本身没有明确的类型。它们的类型只在编译器需要求值的时候被推测。



### 类型别名

类型别名（type aliases）就是给现有类型,定义另一个名字。

使用`typealias`关键字来定义类型别名。

当你想要给现有类型起一个更有意义的名字时，类型别名非常有用。假设你正在处理特定长度的外部资源的数据：

```
typealias AudioSample = UInt16
```

定义了一个类型别名之后，你可以在任何使用原始名的地方使用别名：

```
var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound 现在是 0
```

本例中，`AudioSample`被定义为`UInt16`的一个别名。因为它是别名，`AudioSample.min`实际上是`UInt16.min`，所以会给`maxAmplitudeFound`赋一个初值`0`。

### 布尔值

Swift 有一个基本的布尔（Boolean）类型，叫做`Bool`。布尔值指逻辑上的值，因为它们只能是真或者假。Swift 有两个布尔常量，`true`和`false`：

```
let orangesAreOrange = true
let turnipsAreDelicious = false
```


如果你在需要使用`Bool`类型的地方使用了非布尔值，Swift 的类型安全机制会报错。
下面的例子会报告一个编译时错误：

```
let i = 1
if i {
    // 这个例子不会通过编译，会报错
}
```

然而，下面的例子是合法的：

```
let i = 1
if i == 1 {
    // 这个例子会编译成功
}
```

`i == 1`的比较结果是`Bool`类型，所以第二个例子可以通过类型检查。类似`i == 1`这样的比较，请参考[基本操作符](http://wiki.jikexueyuan.com/project/swift/chapter2/05_Control_Flow.html)。和 Swift 中的其他类型安全的例子一样，这个方法可以避免错误，并保证这块代码的意图总是清晰的。

### 元组

*元组（tuples）*把多个值组合成一个复合值。

>元组内的值可以是任意类型，并不要求是相同类型。

下面这个例子中，`(404, "Not Found")`是一个描述 *HTTP 状态码（HTTP status code）*的元组。

HTTP 状态码是当你请求网页的时候 web 服务器返回的一个特殊值。如果你请求的网页不存在就会返回一个`404 Not Found`状态码。

```
let http404Error = (404, "Not Found")
// http404Error 的类型是 (Int, String)，值是 (404, "Not Found")
```

`(404, "Not Found")`元组把一个`Int`值和一个`String`值组合起来表示 HTTP 状态码的两个部分：一个数字和一个人类可读的描述。这个元组可以被描述为: “一个类型为`(Int, String)`的元组”。

#### 元祖的内容分解

你可以将一个元组的内容分解（decompose）成单独的常量和变量，然后你就可以正常使用它们了：

    let (statusCode, statusMessage) = http404Error
    print("The status code is \(statusCode)")
    // 输出 "The status code is 404"
    print("The status message is \(statusMessage)")
    // 输出 "The status message is Not Found"
    
如果你只需要一部分元组值，分解的时候可以把要忽略的部分用下划线（_）标记：

    let (justTheStatusCode, _) = http404Error
    print("The status code is \(justTheStatusCode)")
    // 输出 "The status code is 404"


#### 访问元祖的单个元素
你还可以通过下标来访问元组中的单个元素，下标从零开始：

```
print("The status code is \(http404Error.0)")
// 输出 "The status code is 404"
print("The status message is \(http404Error.1)")
// 输出 "The status message is Not Found"
```

你可以在定义元组的时候给单个元素命名：

```
let http200Status = (statusCode: 200, description: "OK")
```

给元组中的元素命名后，你可以通过名字来获取这些元素的值：

```
print("The status code is \(http200Status.statusCode)")
// 输出 "The status code is 200"
print("The status message is \(http200Status.description)")
// 输出 "The status message is OK"
```

PS:作为函数返回值时，元组非常有用。一个用来获取网页的函数可能会返回一个`(Int, String)`元组来描述是否获取成功。和只能返回一个类型的值比较起来，一个包含两个不同类型值的元组可以让函数的返回信息更有用。请参考[函数参数与返回值](http://wiki.jikexueyuan.com/project/swift/chapter2/06_Functions.html#Function_Parameters_and_Return_Values)。

> 注意：
> 元组在临时组织值的时候很有用，但是并不适合创建复杂的数据结构。如果你的数据结构并不是临时使用，请使用类或者结构体而不是元组。请参考[类和结构体](http://wiki.jikexueyuan.com/project/swift/chapter2/09_Classes_and_Structures.html)。



## Day2  2016/08/11

知易行难，在工作之余，抽出时间来学习swift，并不像之前想象的轻松。

继续基础部分之旅。

### 可选类型

使用可选类型（optionals）来处理值可能缺失的情况。

可选类型表示：

`有值，等于 x`或`没有值

>注意：
C 和 Objective-C 中并没有可选类型这个概念。

>最接近的是 Objective-C 中的一个特性，一个方法要不返回一个对象要不返回nil，nil表示“缺少一个合法的对象”。

>然而，这只对对象起作用——对于结构体，基本的 C 类型或者枚举类型不起作用。对于这些类型，Objective-C 方法一般会返回一个特殊值（比如NSNotFound）来暗示值缺失。这种方法假设方法的调用者知道并记得对特殊值进行判断。然而，Swift 的可选类型可以让你暗示_任意类型_的值缺失，并不需要一个特殊值。

例如：

	let possibleNumber = "123"
	let convertedNumber = Int(possibleNumber)
	// convertedNumber 被推测为类型 "Int?"， 或者类型 "optional Int"

这里Int()返回的，肯定是一个int类型的值，但如果里面转化的字符为”hello,world“这样的形式，就会转化失败。所以它返回一个可选类型（optional）Int，而不是一个Int。

一个`可选的Int`被写作`Int?`，而不是一个`Int`。

问号暗示包含的值是可选类型，也就是说：可能包含Int值，或者不包含值（如之前所说，可能有值为Int类型，或者没有。并不能包含其他任何值，比如Bool值或者String值。只能是Int或者什么都没有。）


#### nil
你可以给可选(Optional)变量赋值为nil,表示它没有值

	var serverResponseCode: Int? = 404
	// serverResponseCode 包含一个可选的 Int 值 404
	serverResponseCode = nil
	// serverResponseCode 现在不包含值

>注意：

>nil不能用于`非可选`的常量和变量。如果你的代码中有常量或者变量需要处理值缺失的情况，请把它们声明成对应的可选类型。也就说，nil只能用于可选(optional)类型。

如果你声明一个可选常量或者变量但是没有赋值，它们会自动被设置为`nil`：

	var surveyAnswer: String?
	// surveyAnswer 被自动设置为 nil

>注意：
>Swift 的nil和 Objective-C 中的nil并不一样。在 Objective-C 中，nil是一个指向不存在对象的指针。在 Swift 中，nil不是指针——它是一个确定的值，用来表示值缺失。任何类型的可选状态都可以被设置为nil，不只是对象类型。

#### if语句以及强制解析

你可以使用`if`语句和`nil`比较来判断一个可选值是否包含值。你可以使用“相等”(`==`)或“不等”(`!=`)来执行比较。

如果可选类型有值，它将不等于`nil`:

```
if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
// 输出 "convertedNumber contains some integer value."
```

你可以在可选(Optional)的名字后面加一个感叹号（`!`）来获取值。前提是，你得确定可选类型，这个时候是一定有值的。这被称为可选值的*强制解析（forced unwrapping）*：

```
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
// 输出 "convertedNumber has an integer value of 123."
```

>注意：
>使用`!`来获取一个不存在的可选值会导致运行时错误。使用`!`来强制解析值之前，一定要确定可选包含一个非`nil`的值

#### 可选绑定

使用_可选绑定（optional binding）_来判断可选类型是否包含值.

如果包含,就把值赋给一个临时常量或者变量。可选绑定（optional binding）可以用在`if`和`while`语句中，这条语句不仅可以用来判断可选类型中是否有值，同时可以将可选类型中的值赋给一个常量或者变量。

像下面这样在`if`语句中写一个可选绑定：

```
if let constantName = someOptional {
    statements
}
```

你可以像上面这样使用可选绑定来重写`possibleNumber`这个[例子](http://wiki.jikexueyuan.com/project/swift/chapter2/01_The_Basics.html#optionals)：

```
if let actualNumber = Int(possibleNumber) {
    print("\'\(possibleNumber)\' has an integer value of \(actualNumber)")
} else {
    print("\'\(possibleNumber)\' could not be converted to an integer")
}
// 输出 "'123' has an integer value of 123"
```

这段代码可以被理解为：

“如果`Int(possibleNumber)`返回的可选`Int`包含一个值，创建一个叫做`actualNumber`的新常量并将可选包含的值赋给它。”

如果转换成功，actualNumber常量可以在if语句的第一个分支中使用。它已经被可选类型 包含的 值初始化过，所以不需要再使用`!`后缀来获取它的值。

你可以包含多个可选绑定在`if`语句中，并使用`where`子句做布尔值判断。

```
if let firstNumber = Int("4"), secondNumber = Int("42") where firstNumber < secondNumber {
    print("\(firstNumber) < \(secondNumber)")
}
// prints "4 < 42"
```

#### 隐式解析可选类型

如上所述，可选类型暗示了常量或者变量可以“没有值”。

可选(Optional)可以通过`if`语句来判断是否有值，如果`有值`的话可以通过`可选绑定`来解析值。

有时候在程序架构中，第一次被赋值之后，可以确定一个*可选类型总会有值*。在这种情况下，每次都要判断和解析可选值,是非常`低效`的，因为可以确定它总会有值。

这种类型的可选状态被定义为隐式解析可选类型（implicitly unwrapped optionals）。把想要用作可选的类型的后面的问号（`String?`）改成感叹号（`String!`）来声明一个隐式解析可选类型。

当可选类型被第一次赋值之后就可以确定之后一直有值的时候，隐式解析可选类型非常有用。隐式解析可选类型主要被用在 Swift 中类的构造过程中，请参考[无主引用以及隐式解析可选属性](http://wiki.jikexueyuan.com/project/swift/chapter2/16_Automatic_Reference_Counting.html#unowned_references_and_implicitly_unwrapped_optional_properties)。

可选类型`String`和隐式解析可选类型`String`之间的区别：

```
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // 需要惊叹号来获取值

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString  // 不需要感叹号
```

你可以把隐式解析可选类型当做一个可以自动解析的可选类型。你要做的只是声明的时候把感叹号放到类型的结尾，而不是每次取值的可选名字的结尾。

你仍然可以把`隐式解析可选类型`当做普通可选类型来判断它是否包含值：

```
if assumedString != nil {
    print(assumedString)
}
// 输出 "An implicitly unwrapped optional string."
```

你也可以在`可选绑定`中,使用`隐式解析可选类型`来检查并解析它的值：

```
if let definiteString = assumedString {
    print(definiteString)
}
// 输出 "An implicitly unwrapped optional string."
```

> 注意：
> 如果一个变量之后可能变成`nil`的话请不要使用隐式解析可选类型。如果你需要在变量的生命周期中判断是否是`nil`的话，请使用普通可选类型。

### 错误处理

你可以使用*错误处理(error handling)*来应对程序执行中可能会遇到的错误条件。

相对于可选中运用值的存在与缺失,表达函数的成功与失败，错误处理可以推断失败的原因，并传播至程序的其他部分。

当一个函数遇到错误条件，它能报错。调用函数的地方能抛出错误消息并合理处理。

```
func canThrowAnError() throws {
    // 这个函数有可能抛出错误
}
```

一个函数可以通过在声明中添加`throws`关键词来抛出错误消息。

当你的函数能抛出错误消息时, 你应该在表达式中前置`try`关键词。

```
do {
    try canThrowAnError()
    // 没有错误消息抛出
} catch {
    // 有一个错误消息抛出
}
```

一个`do`语句创建了一个新的包含作用域,使得错误能被传播到一个或多个`catch`从句。

这里有一个错误处理如何用来应对不同错误条件的例子。

```
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch Error.OutOfCleanDishes {
    washDishes()
} catch Error.MissingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

在此例中，`makeASandwich()`（做一个三明治）函数会抛出一个错误消息如果没有干净的盘子或者缺失某个原料。因为`makeASandwich()`抛出错误，函数调用被包裹在`try`表达式中。

将函数包裹在一个`do`语句中,任何被抛出的错误,都会被传播到提供的`catch`从句中。

如果没有错误被抛出, `eatASandwich()`函数会被调用。

如果一个匹配`Error.OutOfCleanDishes`的错误被抛出,`washDishes`函数会被调用。

如果一个匹配`Error.MissingIngredients`的错误被抛出，`buyGroceries(_:)`函数会被调用，并且使用`catch`所捕捉到的关联值`[String]`作为参数。

### 断言

可选类型可以让你判断值是否存在，你可以在代码中优雅地处理值缺失的情况。然而，在某些情况下，如果值缺失或者值并不满足特定的条件，你的代码可能没办法继续执行。这时，你可以在你的代码中触发一个_断言（assertion）_来结束代码运行并通过调试来找到值缺失的原因。

#### 使用断言进行调试

断言会在运行时判断一个逻辑条件是否为`true`。从字面意思来说，断言“断言”一个条件是否为真。你可以使用断言来保证在运行其他代码之前，某些重要的条件已经被满足。如果条件判断为`true`，代码运行会继续进行；如果条件判断为`false`，代码执行结束，你的应用被终止。

如果你的代码在调试环境下触发了一个断言，比如你在 Xcode 中构建并运行一个应用，你可以清楚地看到不合法的状态发生在哪里并检查断言被触发时你的应用的状态。此外，断言允许你附加一条调试信息。

你可以使用全局`assert(_:_:file:line:)`函数来写一个断言。向这个函数传入一个结果为`true`或者`false`的表达式以及一条信息，当表达式的结果为`false`的时候这条信息会被显示：

```
let age = -3
assert(age >= 0, "A person's age cannot be less than zero")
// 因为 age < 0，所以断言会触发
```
在这个例子中，只有`age >= 0`为`true`的时候(即`age`的值非负的时候),代码才会继续执行。如果`age`的值是负数，就像代码中那样，`age >= 0`为`false`，断言被触发，终止应用。

如果不需要断言信息，可以省略，就像这样：

    assert(age >= 0)


> 注意：
> 当代码使用优化编译的时候，断言将会被禁用，例如在 Xcode 中，使用默认的 target Release 配置选项来 build 时，断言会被禁用。



### 何时使用断言

当条件`可能为假`时使用断言，但是最终一定要*保证条件为真*，这样你的代码才能继续运行。断言的适用情景：

* 整数类型的下标索引,被传入一个自定义下标实现，但是下标索引值可能太小或者太大。
* 需要给函数传入一个值，但是非法的值可能导致函数不能正常执行。
* 一个可选值现在是`nil`，但是后面的代码运行需要一个非`nil`值。

请参考[下标](http://wiki.jikexueyuan.com/project/swift/chapter2/12_Subscripts.html)和[函数](http://wiki.jikexueyuan.com/project/swift/chapter2/06_Functions.html)。

> 注意：
> `断言`可能导致你的应用终止运行，应当仔细设计你的代码让`非法条件`不会出现。
> 然而，在你的应用发布之前，有时候`非法条件`可能出现，这时`断言`可以快速发现问题。


## Day3 2016/08/12
之前的许多概念，通读下来，完全的复制粘贴。
接下来试着组织语言，进行消化。
### 基本运算符
运算符分为一元、二元和三元运算符。

> 一元运算符
> 
>一元运算符，对单一操作对象操作（如 `-a`）。
>
>一元运算符分`前置运算符`和`后置运算符`。
>
>前置运算符需紧跟在操作对象之前（如 `!b`），后置运算符需紧跟在操作对象之后（如 `c!`）。
>
> 二元运算符
>
>二元运算符，操作两个操作对象（如 `2 + 3`）。
>
>二元运算符是中置的，因为它们出现在两个操作对象之间。
>
> 三元运算符
>
>三元运算符，操作三个操作对象。
>和 C 语言一样，Swift 只有一个三元运算符，就是三目运算符（`a ? b : c`）。

受运算符影响的值叫`操作数`，在表达式 `1 + 2` 中，加号 `+` 是二元运算符，它的两个操作数是值 `1` 和 `2`。

#### 赋值运算符
赋值运算符（=）`不返回值`，以防止把想要判断相等运算符（==）的地方写成赋值符导致的错误。(与之相反，加减乘除等算术运算符都会返回值)

Swift 的赋值操作并不返回任何值。以下代码是错误的：

```
if x = y {
    // 此句错误, 因为 x = y 并不返回任何值。无真无假。
}
```

这个特性使你无法把（==）错写成（=），由于 if x = y 是错误代码，Swift 能帮你避免此类错误发生。

#### 算术运算符
Swift 默认情况下,不允许在数值运算中出现溢出情况。但是你可以使用 Swift 的`溢出运算符`来实现溢出运算（如 a &+ b）。

swift中的加号运算符，可以用于字符串的拼接:

    "hello, " + "world"  // 等于 "hello, world"

#### 求余运算符
这个也是比较常见的运算符号，顾名思义，求余运算（a % b）将返回a除以b的余数。

在对负数 b 求余时，b 的符号会被忽略。这意味着 a % b 和 a % -b 的结果是相同的:

    let a = 8 % 3;
    let b = 8 % -3;
    if a==b {
        print("\(a)等于\(b)")
    }
    //输出“2等于2”

值得一提的是，swift还可以对`浮点数`进行求余运算。

    8 % 2.5   // 等于 0.5


#### 组合赋值运算符
Swift 提供把其他运算符和赋值运算（`=`）组合的组合赋值运算符，组合加运算（`+=`）是其中一个例子：

```
var a = 1
a += 2
// a 现在是 3
```

表达式 `a += 2` 是 `a = a + 2` 的简写，一个组合加运算（+=），就是把加法运算和赋值运算组合成进一个运算符里，同时完成两个运算任务。

依次类推，组合乘运算`a *= b`等于`a = a * b `:

```
var myVariable = 50
myVariable *= 2;
//此时myVariable的值为100
```

> 注意：
> 复合赋值运算，和赋值运算一样，也没有返回值。
> `let b = a += 2`这类代码是错误。这不同于上面提到的自增和自减运算符。

#### 比较运算符

当元组中的值可以比较时，你也可以使用这些运算符来比较它们的大小。

例如，因为 Int 和 String 类型的值可以比较，所以类型为 (Int, String) 的元组也可以被比较。

比较`元组大小`会按照从左到右、逐值比较的方式，直到发现有两个值不等时停止。如果所有的值都相等，那么这一对元组我们就称它们是相等的。例如：

```
(1, "zebra") < (2, "apple")   // true，因为 1 小于 2
(3, "apple") < (3, "bird")    // true，因为 3 等于 3，但是 apple 小于 bird
(4, "dog") == (4, "dog")      // true，因为 4 等于 4，dog 等于 dog
```

>注意： Swift 标准库只能比较七个以内元素的元组比较函数。如果你的元组元素超过七个时，你需要自己实现比较运算符。

#### 空合运算符(Nil Coalescing Operator)
空合运算符（a ?? b）将对可选类型 a 进行空判断,表达式 a 必须是 Optional 类型,默认值 b 的类型必须要和 a 存储值的类型保持一致。

空合运算符是对以下代码的简短表达方法：

```
a != nil ? a! : b
```

上述代码使用了三目运算符。当可选类型 `a` 的值不为空时，进行强制解封（`a!`），访问 `a` 中的值；反之返回默认值`b`。无疑空合运算符（`??`）提供了一种更为优雅的方式去封装条件判断和解封两种行为，显得简洁以及更具可读性。

下文例子采用空合运算符，实现了在默认颜色名和可选自定义颜色名之间抉择：

```
let defaultColorName = "red"
var userDefinedColorName: String?   //默认值为 nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName 的值为空，所以 colorNameToUse 的值为 "red"
```

`userDefinedColorName` 变量被定义为一个可选的 `String` 类型，默认值为 `nil`。由于 `userDefinedColorName` 是一个可选类型，我们可以使用空合运算符去判断其值。在上一个例子中，通过空合运算符为一个名为 `colorNameToUse`的变量赋予一个字符串类型初始值。 由于 `userDefinedColorName` 值为空，因此表达式 `userDefinedColorName ?? defaultColorName` 返回 `defaultColorName` 的值，即 `red`。

另一种情况，分配一个非空值（`non-nil`）给 `userDefinedColorName`，再次执行空合运算，运算结果为封包在`userDefaultColorName` 中的值，而非默认值。

```
userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName 非空，因此 colorNameToUse 的值为 "green"
```

#### 区间运算符
##### 闭区间运算符

闭区间运算符（`a...b`）定义一个包含从 `a` 到 `b`（包括 `a` 和 `b`）的所有值的区间。`a` 的值不能超过 `b`。 ‌ 闭区间运算符在迭代一个区间的所有值时是非常有用的，如在 `for-in` 循环中：

```
for index in 1...5 {
    print("\(index) * 5 = \(index * 5)")
}
// 1 * 5 = 5
// 2 * 5 = 10
// 3 * 5 = 15
// 4 * 5 = 20
// 5 * 5 = 25
```
##### 半开区间运算符

半开区间（`a..<b`）定义一个从 `a` 到 `b` 但不包括 `b` 的区间。 之所以称为半开区间，是因为该区间包含第一个值而不包括最后的值。

半开区间的实用性在于当你使用一个从 0 开始的列表（如数组）时，非常方便地从0数到列表的长度。

```
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("第 \(i + 1) 个人叫 \(names[i])")
}
// 第 1 个人叫 Anna
// 第 2 个人叫 Alex
// 第 3 个人叫 Brian
// 第 4 个人叫 Jack
```

数组有 4 个元素，但 `0..<count` 只数到3（最后一个元素的下标），因为它是半开区间。
### 字符串和字符

#### 初始化空字符串 (Initializing an Empty String)

要创建一个空字符串作为初始值，可以将空的字符串字面量赋值给变量，也可以初始化一个新的`String`实例：

```
var emptyString = ""               // 空字符串字面量
var anotherEmptyString = String()  // 初始化方法
// 两个字符串均为空并等价。
```

您可以通过检查其`Bool`类型的`isEmpty`属性来判断该字符串是否为空：

```
if emptyString.isEmpty {
    print("Nothing to see here")
}
// 打印输出："Nothing to see here"
```



#### 字符串可变性 (String Mutability)

您可以通过将一个特定字符串分配给一个变量来对其进行修改，或者分配给一个常量来保证其不会被修改：

```
var variableString = "Horse"
variableString += " and carriage"
// variableString 现在为 "Horse and carriage"

let constantString = "Highlander"
constantString += " and another Highlander"
// 这会报告一个编译错误 (compile-time error) - 常量字符串不可以被修改。
```

> 注意： 在 Objective-C 和 Cocoa 中，您需要通过选择两个不同的类(`NSString`和`NSMutableString`)来指定字符串是否可以被修改。



#### 字符串是值类型（Strings Are Value Types）

Swift 的`String`类型是值类型。 如果您创建了一个新的字符串，那么当其进行常量、变量赋值操作，或在函数/方法中传递时，会进行值拷贝。 任何情况下，都会对已有字符串值创建新副本，并对该新副本进行传递或赋值操作。 值类型在 [结构体和枚举是值类型](http://wiki.jikexueyuan.com/project/swift/chapter2/09_Classes_and_Structures.html#structures_and_enumerations_are_value_types) 中进行了详细描述。

Swift 默认字符串拷贝的方式保证了在函数/方法中传递的是字符串的值。 很明显无论该值来自于哪里，都是您独自拥有的。 您可以确信传递的字符串不会被修改，除非你自己去修改它。

在实际编译时，Swift 编译器会优化字符串的使用，使实际的复制只发生在绝对必要的情况下，这意味着您将字符串作为值类型的同时可以获得极高的性能。

### 集合类型

Swift 语言提供`Arrays`、`Sets`和`Dictionaries`三种基本的集合类型用来存储集合数据。数组（Arrays）是有序数据的集。集合（Sets）是无序无重复数据的集。字典（Dictionaries）是无序的键值对的集。

#### 数组的简单语法

写 Swift 数组应该遵循像`Array`这样的形式，其中`Element`是这个数组中唯一允许存在的数据类型。我们也可以使用像`[Element]`这样的简单语法。尽管两种形式在功能上是一样的，但是推荐较短的那种，而且在本文中都会使用这种形式来使用数组。



#### 创建一个空数组

我们可以使用构造语法来创建一个由特定数据类型构成的空数组：

```
var someInts = [Int]()
print("someInts is of type [Int] with \(someInts.count) items.")
// 打印 "someInts is of type [Int] with 0 items."
```

注意，通过构造函数的类型，`someInts`的值类型被推断为`[Int]`。

或者，如果代码上下文中已经提供了类型信息，例如一个函数参数或者一个已经定义好类型的常量或者变量，我们可以使用空数组语句创建一个空数组，它的写法很简单：`[]`（一对空方括号）：

```
someInts.append(3)
// someInts 现在包含一个 Int 值
someInts = []
// someInts 现在是空数组，但是仍然是 [Int] 类型的。
```

#### 通过两个数组相加创建一个数组

我们可以使用加法操作符（`+`）来组合两种已存在的相同类型数组。新数组的数据类型会被从两个数组的数据类型中推断出来：

```
var anotherThreeDoubles = [Double](count: 3, repeatedValue: 2.5)
// anotherThreeDoubles 被推断为 [Double]，等价于 [2.5, 2.5, 2.5]

var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles 被推断为 [Double]，等价于 [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```



#### 用字面量构造数组

我们可以使用字面量来进行数组构造，这是一种用一个或者多个数值构造数组的简单方法。字面量是一系列由逗号分割并由方括号包含的数值：

`[value 1, value 2, value 3]`。

下面这个例子创建了一个叫做`shoppingList`并且存储`String`的数组：

```
var shoppingList: [String] = ["Eggs", "Milk"]
// shoppingList 已经被构造并且拥有两个初始项。
```

`shoppingList`变量被声明为“字符串值类型的数组“，记作`[String]`。 因为这个数组被规定只有`String`一种数据结构，所以只有`String`类型可以在其中被存取。 在这里，`shoppinglist`数组由两个`String`值（`"Eggs"` 和`"Milk"`）构造，并且由字面量定义。

## Day4 2016/08/14

### 函数
#### 函数定义和调用

##### 定义
定义一个叫做 `personName` 的 `String` 值，和一个包含给这个人问候语的 `String` 类型的返回值：

```
func sayHello(personName: String) -> String {
    let greeting = "Hello, " + personName + "!"
    return greeting
}
```

所有的这些信息汇总起来成为函数的_定义_，并以 `func` 作为前缀。指定函数返回类型时，用返回箭头 `->`（一个连字符后跟一个右尖括号）后跟返回类型的名称的方式来表示。
##### 调用
上面定义的函数可以在别的地方以一种清晰的方式被调用：

```
print(sayHello("Anna"))
// prints "Hello, Anna!"
print(sayHello("Brian"))
// prints "Hello, Brian!"
```

调用 `sayHello(_:)` 函数时，在圆括号中传给它一个 `String` 类型的实参，例如 `sayHello("Anna")`。

#### 函数参数与返回值
##### 无参函数（Functions Without Parameters）

函数可以没有参数。下面这个函数就是一个无参函数，当被调用时，它返回固定的 `String` 消息：

```
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
// prints "hello, world"
```

尽管这个函数没有参数，但是定义中在函数名后还是需要一对`圆括号`。

>当无参函数被调用时，也需要在函数名后写一对`圆括号`。

##### 多参数函数 (Functions With Multiple Parameters)

函数可以有多种输入参数，这些参数被包含在函数的括号之中，以逗号分隔。

这个函数用一个人名和是否已经打过招呼作为输入，并返回对这个人的适当问候语:

```
func sayHello(personName: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return sayHelloAgain(personName)
    } else {
        return sayHello(personName)
    }
}
print(sayHello("Tim", alreadyGreeted: true))
// prints "Hello again, Tim!"
```

你通过在括号内传递一个`String`参数值和一个标识为`alreadyGreeted`的`Bool`值，使用逗号分隔来调用`sayHello(_:alreadyGreeted:)`函数。

当调用超过一个参数的函数时，第一个参数后的参数根据其对应的参数名称标记.

#### 无返回值函数（Functions Without Return Values）

函数可以没有返回值。下面是 `sayHello(_:)` 函数的另一个版本，叫 `sayGoodbye(_:)`，这个函数直接输出 `String`值，而不是返回它：

```
func sayGoodbye(personName: String) {
    print("Goodbye, \(personName)!")
}
sayGoodbye("Dave")
// prints "Goodbye, Dave!"
```

因为这个函数不需要返回值，所以这个函数的定义中没有返回箭头（->）和返回类型。

> 注意
> 严格上来说，虽然没有返回值被定义，`sayGoodbye(_:)` 函数依然返回了值。没有定义返回类型的函数会返回特殊的值，叫 `Void`。它其实是一个空的元组（tuple），没有任何元素，可以写成`()`。

被调用时，一个函数的返回值可以被忽略：

```
func printAndCount(stringToPrint: String) -> Int {
    print(stringToPrint)
    return stringToPrint.characters.count
}
func printWithoutCounting(stringToPrint: String) {
    printAndCount(stringToPrint)
}
printAndCount("hello, world")
// prints "hello, world" and returns a value of 12
printWithoutCounting("hello, world")
// prints "hello, world" but does not return a value

```

第一个函数 `printAndCount(_:)`，输出一个字符串并返回 `Int` 类型的字符数。第二个函数 `printWithoutCounting`调用了第一个函数，但是忽略了它的返回值。当第二个函数被调用时，消息依然会由第一个函数输出，但是返回值不会被用到。

> 注意
> 返回值可以被忽略，但定义了有返回值的函数必须返回一个值，如果在函数定义底部没有返回任何值，将导致编译错误（compile-time error）。

#### 多重返回值函数（Functions with Multiple Return Values）

你可以用元组（tuple）类型让多个值作为一个复合值从函数中返回。

下面的这个例子中，定义了一个名为`minMax(_:)`的函数，作用是在一个`Int`数组中找出最小值与最大值。

```
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1.. currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

因为元组的成员值已被命名，因此可以通过点语法来检索找到的最小值与最大值：

```
let bounds = minMax([8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")
// prints "min is -6 and max is 109"
```

需要注意的是，元组的成员不需要在元组从函数中返回时命名，因为它们的名字已经在函数返回类型中指定了。

### 闭包 
>我觉得这部分，文档有点啰嗦，找到一篇南峰子大大的解读，觉得不错。原文：[Swift闭包一：闭包基础概念](http://southpeak.github.io/blog/2014/06/27/ios-swift-closures/)

熟悉Objective-C的朋友一定知道Objective-C中的block，iOS在6.0后开始大量使用block。而在swift中，也提供了类似的功能：Closures(在Java等语言中翻译为“闭包”)。

`Closures`是自包含的功能块。它可以捕获和存储其所在上下文的常量和变量的引用。全局函数和嵌套函数其实都是闭包。闭包有以下三种形式：

* 全局函数：有函数名，但不能获取任何外部值
* 嵌套函数：有函数名，同时可以从其上下文中捕获值
* 闭包表达式：以一种轻量级的语法定义的未命名闭包，可以从其上下文中捕获值

#### 闭包表达式

闭包表达式提供了一种更加简洁、专注的方式来实现内嵌函数的功能。闭包表达式的通用格式如下

```
{(parameters) -> return type in
    statement   
}

```

闭包的参数可以是常量、变量、inout、可变参数列表、元组，但是不能提供默认值。返回值可以是通用类型，也可以是元组。闭包实现体位于in关键字后面，该关键字是闭包参数和返回值的声明和实现体的分界。

###### 代码清单1: 使用sort函数对数组进行排序

```
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

// 方法1：使用普通函数(或内嵌函数)提供排序功能
func backwards(s1:String, s2:String) -> Bool {
    return s1 > s2
}

var reversed = sort(names, backwards)

// 方法2：使用闭包表达式提供排序功能
reversed = sort(names, {
        (s1:String, s2:String) -> Bool in
            return s1 > s2
    })

// 方法3：类型推断,省略闭包表达式的参数及返回类型
reversed = sort(names, { s1, s2 in return s1 > s2})

// 方法4：单一表达式：省略return关键字
reversed = sort(names, { s1, s2 in s1 > s2 })

// 方法5：速记参数名
reversed = sort(names, { $0 > $1 })

// 方法6：操作符函数
reversed = sort(names, >)

```

swift标准库提供了sort用来对数据进行排序，它包含两个参数：

1. 待排序的已知类型的数组
2. 排序函数(闭包)：带有两个类型相同的参数，并返回Bool值来告知第一个参数是显示排在第二个参数之前还是之后。

代码清单1提供了几种方式来实现sort的排序函数

1. 方法1：使用普通函数(嵌套函数)，这种方法略显示复杂，且代码不够紧凑
2. 方法2：内联闭包表达式，参数和返回值都位于大括号内，而不是外部
3. 方法3：借助于swift强大的类型推断功能，我们甚至可以省略参数和返回值的类型。这样返回箭头->和返回类型都可以省略。在传递闭包给函数时，总是可以推断出参数类型和返回值，所以，我们很少需要明确写出内联闭包的完整格式。
4. 方法4：如果闭包体只有一行代码，则可以省略retrun关键字，让闭包隐式返回单一表达式的值。
5. 方法5：速记(Shorthand)参数名：swift为内联闭包提供了速记参数名，可以通过$0, $1, $2等参数名来索引闭包的参数。如果使用这种参数名，则可以直接省略参数列表，而参数的个数和类型可以自动推断出来。in关键字也可以省略
6. 方法6：更极端的情况是，swift的字符串类型定义了>操作符，该操作符可以看作是带有两个参数的函数，并返回一个Bool值。而这正好符合sort函数的需求，我们可以只是简单的传入一个>，swift可以自动推断出我们想使用的实现。

#### 尾随闭包(Trailing Closures)

如果将闭包作为函数的`最后一个参数`，且闭包的实现体很长，则调用函数时可以使用`尾随闭包`。`尾随闭包`位于参数列表括号的后面。其格式如下：

```
someFunctionThatTakesAClosure() {
    // 尾随闭包实现    
}

```

因此sort函数同样可以如下实现

###### 代码清单2: 使用尾随闭包实现sort函数

```
// 方法7：尾随闭包
reversed = sort(names) { $0 > $1 }

```

另外，如果函数只有一个闭包参数，同时将闭包参数实现为尾随闭包，则在调用函数时可以省略参数列表的()，如代码清单3所示：

###### 代码清单3：函数只有一个闭包参数，同时将闭包参数实现为尾随闭包

```
let strings = numbers.map {
    (var name) -> String in
    var output = ""
    while number > 0 {
        output = digitNames[number % 10]! + output
        number /= 10
    }

    return number
}
```

#### 获取上下文的值
>这一部分本人认为比较重点。

和Objective-C的block一样，闭包可以获取定义它的上下文中常量或变量的值，同时可以在闭包体内引用和修改这些常量或变量的值，*即使定义这些常量或变量的域已经销毁*。

由于内嵌函数也是闭包，因此我们以内嵌函数为例，看看闭包如何获取上下文的常量和变量

###### 代码清单4：获取上下文值

```
func makeIncrementor(amount:Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
    }

    return incrementor
}

```

在*代码清单4*中，内嵌函数incriminator从上下文获取了两个值runningTotal和amount，其中amount是函数makeIncrementor的参数，runningTotal是函数内部定义的变量。

由于incrementor没有修改amount，所以它实际上存储了amount的一份拷贝。而runningTotal在incremetor中被修改了，因此increminator存储了runningTotal的引用，这样确保runningTotal一直有效。

swift决定捕获的值哪些需要`拷贝值`，而哪些只`拷贝引用`。在runningTotal不再使用时，swift负责释放其内存。

如果我们单独看这个函数，会发现看上去*不同寻常*：

```
func incrementor() -> Int {
    runningTotal += amount
    return runningTotal
}
```

`incrementer()`函数并没有任何参数，但是在函数体内访问了`runningTotal`和`amount`变量。这是因为它从外围函数捕获了`runningTotal`和`amount`变量的引用。捕获引用保证了`runningTotal`和`amount`变量在调用完`makeIncrementer`后不会消失，并且保证了在下一次执行`incrementer`函数时，`runningTotal`依旧存在。

> 注意
> 为了优化，如果一个值是不可变的，Swift 可能会改为捕获并保存一份对值的拷贝。
> Swift 也会负责被捕获变量的所有内存管理工作，包括释放不再需要的变量。


###### 代码清单5：makeIncrementor使用

```
let incrementByTen = makeIncrementor(amount:10)

incrementByTen()    // returns a value of 10
incrementByTen()    // returns a value of 20
incrementByTen()    // returns a value of 30

// 定义另一个incrementor，则它有自己独立的runningTotal
let incrementBySeven = makeIncrementor(amount:7)

incrementBySeven()  // returns a value of 7
incrementBySeven()  // returns a value of 14
incrementBySeven()  // returns a value of 21

```

#### 引用类型

在代码清单5中，虽然incrementByTen和incrementBySeven定义为常量，但是闭包仍然可以增加runningTotal的值。这是因为函数和闭包都是引用类型。

当定义一个函数(闭包)常量或变量时，实际上定义的是一个指向函数(闭包)的引用。这意味着如果指定一个闭包给两个不同的常量或变量，则这两个常量和变量将引用同一个函数(闭包)

###### 代码清单6：引用函数(闭包)

```
let incrementByTen = makeIncrementor(amount:10)
incrementByTen()    // returns a value of 10
incrementByTen()    // returns a value of 20
incrementByTen()    // returns a value of 30

let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()  // returns a value of 40

```

这样，就引出另一个问题：循环引用。

##### 闭包循环引用

-------




#### 非逃逸闭包
* `逃逸闭包`是外部是可以访问的, 可以在函数体之外执行。
* `非逃逸闭包`只能在函数体内部访问 ，也就是函数体执行结束之后`非逃逸闭包`也就失效了。


##### 需要逃逸的情况

当闭包作为一个`实际参数`传递给一个函数的时候，我们就说这个闭包`逃逸`了，因为它可以在*函数返回之后被调用*。

通俗点说，从函数中逃逸的意思是将闭包传递给A函数，但是在A函数体中并未执行该闭包，而是A将闭包传递出去，然后另一个函数比如B函数执行时才执行该闭包。

一种能使闭包“逃逸”出函数的方法是，将这个闭包保存在一个函数外部定义的变量中。

举个例子：很多启动**异步操作的函数**接受一个闭包参数作为 `completion handler`。这类函数会在异步操作开始之后立刻返回，但是闭包直到异步操作结束后才会被调用。在这种情况下，闭包需要“逃逸”出函数，因为闭包需要在函数返回之后被调用。例如：

```
var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: () -> Void) {
    completionHandlers.append(completionHandler)
}
```
如示例，闭包加入了数组,通过在外部访问数组元素,从而达到了使用那个闭包的效果
##### 使用@noescape指明不允许逃逸

当你定义接受闭包作为参数的函数时，你可以在参数名之前标注`@noescape`，用来指明这个闭包是不允许“逃逸”出这个函数的。将闭包标注`@noescape`能使编译器知道这个闭包的生命周期（译者注：闭包只能在函数体中被执行，不能脱离函数体执行，所以编译器明确知道运行时的上下文），从而可以进行一些比较激进的优化。

```
func someFunctionWithNoescapeClosure(@noescape closure: () -> Void) {
    closure()
}
```

举个例子，`sort(_:)`方法接受一个用来进行元素比较的闭包作为参数。这个参数被标注了`@noescape`，因为它确保自己在排序结束之后就没用了。


## Day5 2016/08/16

### 枚举
#### 枚举语法

使用`enum`关键词来创建枚举并且把它们的整个定义放在一对大括号内：

```
enum SomeEnumeration {
    // 枚举定义放在这里
}
```

下面是用枚举表示指南针四个方向的例子：

```
enum CompassPoint {
    case North
    case South
    case East
    case West
}
```

枚举中定义的值（如 `North`，`South`，`East`和`West`）是这个枚举的*成员值*（或*成员*）。你使用`case`关键字来定义一个新的枚举成员值。

> 注意
> 与 C 和 Objective-C 不同，Swift 的枚举成员在被创建时不会被赋予一个默认的整型值。在上面的`CompassPoint`例子中，`North`，`South`，`East`和`West`不会被隐式地赋值为`0`，`1`，`2`和`3`。相反，这些枚举成员本身就是完备的值，这些值的类型是已经明确定义好的`CompassPoint`类型。

多个成员值可以出现在同一行上，用逗号隔开：

```
enum Planet {
    case Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune
}
```

每个枚举定义了一个全新的类型。像 Swift 中其他类型一样，它们的名字（例如`CompassPoint`和`Planet`）应该以一个大写字母开头。给枚举类型起一个单数名字而不是复数名字，以便于读起来更加容易理解：

```
var directionToHead = CompassPoint.West
```

`directionToHead`的类型可以在它被`CompassPoint`的某个值初始化时推断出来。一旦`directionToHead`被声明为`CompassPoint`类型，你可以使用更简短的点语法将其设置为另一个`CompassPoint`的值：

```
directionToHead = .East
```

当`directionToHead`的类型已知时，再次为其赋值可以省略枚举类型名。在使用具有显式类型的枚举值时，这种写法让代码具有更好的可读性。

#### 关联值（Associated Values）

有时候能够把其他类型的`关联值`和`成员值`一起存储起来会很有用。这能让你连同`成员值`一起存储额外的自定义信息，并且你每次在代码中使用该枚举成员时，还可以修改这个关联值。

你可以定义 Swift 枚举来存储任意类型的关联值，如果需要的话，每个枚举成员的关联值类型可以各不相同。

`枚举`的这种特性跟其他语言中的可识别联合（discriminated unions），标签联合（tagged unions），或者变体（variants）相似。

例如，假设一个库存跟踪系统需要利用两种不同类型的条形码来跟踪商品。有些商品上标有使用`0`到`9`的数字的 UPC-A 格式的一维条形码。每一个条形码都有一个代表“数字系统”的数字，该数字后接五位代表“厂商代码”的数字，接下来是五位代表“产品代码”的数字。最后一个数字是“检查”位，用来验证代码是否被正确扫描：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/barcode_UPC_2x.png)

其他商品上标有 QR 码格式的二维码，它可以使用任何 ISO 8859-1 字符，并且可以编码一个最多拥有 2,953 个字符的字符串：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/barcode_QR_2x.png)

这便于库存跟踪系统用包含四个整型值的元组存储 UPC-A 码，以及用任意长度的字符串储存 QR 码。

在 Swift 中，使用如下方式定义表示两种商品条形码的枚举：

```
enum Barcode {
    case UPCA(Int, Int, Int, Int)
    case QRCode(String)
}
```

以上代码可以这么理解：

“定义一个名为`Barcode`的枚举类型，它的一个成员值是具有`(Int，Int，Int，Int)`类型 *关联值* 的`UPCA`，另一个成员值是具有`String`类型 *关联值* 的`QRCode`。”

这个定义不提供任何`Int`或`String`类型的关联值，它只是定义了，当`Barcode`常量和变量等于`Barcode.UPCA`或`Barcode.QRCode`时，可以存储的关联值的类型。

然后可以使用任意一种条形码类型创建新的条形码，例如：

```
var productBarcode = Barcode.UPCA(8, 85909, 51226, 3)
```

上面的例子创建了一个名为`productBarcode`的变量，并将`Barcode.UPCA`赋值给它，关联的元组值为`(8, 85909, 51226, 3)`。

同一个商品可以被分配一个不同类型的条形码，例如：

```
productBarcode = .QRCode("ABCDEFGHIJKLMNOP")
```

这时，原始的`Barcode.UPCA`和其整数关联值被新的`Barcode.QRCode`和其字符串关联值所替代。`Barcode`类型的常量和变量可以存储一个`.UPCA`或者一个`.QRCode`（连同它们的关联值），但是在同一时间只能存储这两个值中的一个。

像先前那样，可以使用一个 switch 语句来检查不同的条形码类型。然而，这一次，关联值可以被提取出来作为 switch 语句的一部分。你可以在`switch`的 case 分支代码中提取每个关联值作为一个常量（用`let`前缀）或者作为一个变量（用`var`前缀）来使用：

```
switch productBarcode {
case .UPCA(let numberSystem, let manufacturer, let product, let check):
    print("UPC-A: \(numberSystem), \(manufacturer), \(product), \(check).")
case .QRCode(let productCode):
    print("QR code: \(productCode).")
}
// 输出 "QR code: ABCDEFGHIJKLMNOP."
```

如果一个枚举成员的所有关联值都被提取为常量，或者都被提取为变量，为了简洁，你可以只在成员名称前标注一个`let`或者`var`：

```
switch productBarcode {
case let .UPCA(numberSystem, manufacturer, product, check):
    print("UPC-A: \(numberSystem), \(manufacturer), \(product), \(check).")
case let .QRCode(productCode):
    print("QR code: \(productCode).")
}
// 输出 "QR code: ABCDEFGHIJKLMNOP."
```


### 类和结构体

#### 定义语法

类和结构体有着类似的定义方式。我们通过关键字`class`和`struct`来分别表示类和结构体，并在一对大括号中定义它们的具体内容：

```
class SomeClass {
    // class definition goes here
}
struct SomeStructure {
    // structure definition goes here
}
```

> 注意
> 在你每次定义一个新类或者结构体的时候，实际上你是定义了一个新的 Swift 类型。因此请使用`UpperCamelCase`这种方式来命名（如`SomeClass`和`SomeStructure`等），以便符合标准 Swift 类型的大写命名风格（如`String`，`Int`和`Bool`）。相反的，请使用`lowerCamelCase`这种方式为属性和方法命名（如`framerate`和`incrementCount`），以便和类型名区分。

以下是定义结构体和定义类的示例：

```
struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```

在上面的示例中我们定义了一个名为`Resolution`的结构体，用来描述一个显示器的像素分辨率。这个结构体包含了两个名为`width`和`height`的`存储属性`。`存储属性`是被捆绑和存储在类或结构体中的常量或变量。当这两个属性被初始化为整数`0`的时候，它们会被推断为`Int`类型。

在上面的示例中我们还定义了一个名为`VideoMode`的类，用来描述一个视频显示器的特定模式。这个类包含了四个变量存储属性。第一个是`分辨率`，它被初始化为一个新的`Resolution`结构体的实例，属性类型被推断为`Resolution`。新`VideoMode`实例同时还会初始化其它三个属性，它们分别是，初始值为`false`的`interlaced`，初始值为`0.0`的`frameRate`，以及值为可选`String`的`name`。`name`属性会被自动赋予一个默认值`nil`，意为“没有`name`值”，因为它是一个可选类型。


#### 类和结构体实例
如上，我们可以分别生成一个结构体(struct)`Resolution`和类(class)`VideoMode`的实例。

生成它们的实例的语法，非常相似：

```
let someRosolution=Resolution()
let someVideoMode=VideoMode()
``` 

结构体和类都使用构造器语法来生成新的实例。构造器语法的最简单形式是在结构体或者类的类型名称后跟随一对空括号，如`Resolution()`或`VideoMode()`。通过这种方式所创建的类或者结构体实例，其属性均会被初始化为默认值。

#### 结构体类型的成员逐一构造器（Memberwise Initializers for Structure Types）

所有结构体都有一个自动生成的_成员逐一构造器_，用于初始化新结构体实例中成员的属性。新实例中各个属性的初始值可以通过属性的名称传递到成员逐一构造器之中：

```
let vga = Resolution(width:640, height: 480)
```

与结构体不同，类实例没有默认的成员逐一构造器。

#### 结构体和枚举是值类型

>值类型被赋予给一个变量、常量或者被传递给一个函数的时候，其值会被拷贝。

在之前的章节中，我们已经大量使用了值类型。实际上，在 Swift 中，所有的基本类型：整数（Integer）、浮点数（floating-point）、布尔值（Boolean）、字符串（string)、数组（array）和字典（dictionary），都是值类型，并且在底层都是以结构体的形式所实现。

在 Swift 中，所有的结构体和枚举类型都是值类型。这意味着它们的实例，以及实例中所包含的任何值类型属性，在代码中传递的时候都会被复制。

请看下面这个示例，其使用了前一个示例中的`Resolution`结构体：

```
let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
```

在以上示例中，声明了一个名为`hd`的常量，其值为一个初始化为全高清视频分辨率（`1920` 像素宽，`1080` 像素高）的`Resolution`实例。

然后示例中又声明了一个名为`cinema`的变量，并将`hd`赋值给它。因为`Resolution`是一个结构体，所以`cinema`的值其实是`hd`的一个拷贝副本，而不是`hd`本身。尽管`hd`和`cinema`有着相同的宽（width）和高（height），但是在幕后它们是两个完全不同的实例。

下面，为了符合数码影院放映的需求（`2048` 像素宽，`1080` 像素高），`cinema`的`width`属性需要作如下修改：

```
cinema.width = 2048
```

这里，将会显示`cinema`的`width`属性确已改为了`2048`：

```
print("cinema is now  \(cinema.width) pixels wide")
// 输出 "cinema is now 2048 pixels wide"
```

然而，初始的`hd`实例中`width`属性还是`1920`：

```
print("hd is still \(hd.width) pixels wide")
// 输出 "hd is still 1920 pixels wide"
```

在将`hd`赋予给`cinema`的时候，实际上是将`hd`中所存储的值进行拷贝，然后将拷贝的数据存储到新的`cinema`实例中。结果就是两个完全独立的实例碰巧包含有相同的数值。由于两者相互独立，因此将`cinema`的`width`修改为`2048`并不会影响`hd`中的`width`的值。

#### 类是引用类型

>与值类型不同，引用类型在被赋予到一个变量、常量或者被传递到一个函数时，其值不会被拷贝。
>因此，引用的是已存在的实例本身而不是其拷贝。

请看下面这个示例，其使用了之前定义的`VideoMode`类：

```
let tenEighty = VideoMode()
tenEighty.resolution = hd
tenEighty.interlaced = true
tenEighty.name = "1080i"
tenEighty.frameRate = 25.0
```

以上示例中，声明了一个名为`tenEighty`的常量，其引用了一个`VideoMode`类的新实例。在之前的示例中，这个视频模式（video mode）被赋予了HD分辨率（`1920`*`1080`）的一个拷贝（即`hd`实例）。同时设置为`interlaced`，命名为`“1080i”`。最后，其帧率是`25.0`帧每秒。

然后，`tenEighty`被赋予名为`alsoTenEighty`的新常量，同时对`alsoTenEighty`的帧率进行修改：

```
let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0
```

因为类是引用类型，所以`tenEight`和`alsoTenEight`实际上引用的是相同的`VideoMode`实例。换句话说，它们是同一个实例的两种叫法。

下面，通过查看`tenEighty`的`frameRate`属性，我们会发现它正确的显示了所引用的`VideoMode`实例的新帧率，其值为`30.0`：

```
print("The frameRate property of tenEighty is now \(tenEighty.frameRate)")
// 输出 "The frameRate property of theEighty is now 30.0"
```

需要注意的是`tenEighty`和`alsoTenEighty`被声明为常量而不是变量。然而你依然可以改变`tenEighty.frameRate`和`alsoTenEighty.frameRate`，因为`tenEighty`和`alsoTenEighty`这两个常量的值并未改变。它们并不“存储”这个`VideoMode`实例，而仅仅是对`VideoMode`实例的引用。所以，改变的是被引用的`VideoMode`的`frameRate`属性，而不是引用`VideoMode`的常量的值。

#### 恒等运算符

因为类是引用类型，有可能有多个常量和变量在幕后同时引用同一个类实例。（对于结构体和枚举来说，这并不成立。因为它们作为值类型，在被赋予到常量、变量或者传递到函数时，其值总是会被拷贝。）

如果能够判定两个常量或者变量是否引用`同个类实例`将会很有帮助。为了达到这个目的，Swift 内建了两个恒等运算符：

* 等价于（`===`）
* 不等价于（`!==`）

运用这两个运算符检测两个常量或者变量是否引用同一个实例：

```
if tenEighty === alsoTenEighty {
    print("tenEighty and alsoTenEighty refer to the same Resolution instance.")
}
//输出 "tenEighty and alsoTenEighty refer to the same Resolution instance."
```

请注意，“等价于”（用三个等号表示，`===`）与“等于”（用两个等号表示，`==`）的不同：

* “等价于”表示两个类类型（class type）的常量或者变量引用同一个类实例。
* “等于”表示两个实例的值“相等”或“相同”，判定时要遵照设计者定义的评判标准，因此相对于“相等”来说，这是一种更加合适的叫法。

当你在定义你的自定义类和结构体的时候，你有义务来决定判定两个实例“相等”的标准。

#### 类和结构体的选择

在你的代码中，你可以使用类和结构体来定义你的自定义数据类型。

然而，结构体实例总是通过值传递，类实例总是通过引用传递。这意味两者适用不同的任务。当你在考虑一个工程项目的数据结构和功能的时候，你需要决定每个数据结构是定义成类还是结构体。

按照通用的准则，当符合一条或多条以下条件时，请考虑构建结构体：

* 该数据结构的主要目的是用来封装少量相关简单数据值。
* 有理由预计该数据结构的实例在被赋值或传递时，封装的数据将会被拷贝而不是被引用。
* 该数据结构中储存的值类型属性，也应该被拷贝，而不是被引用。
* 该数据结构不需要去继承另一个既有类型的属性或者行为。

举例来说，以下情境中适合使用结构体：

* 几何形状的大小，封装一个`width`属性和`height`属性，两者均为`Double`类型。
* 一定范围内的路径，封装一个`start`属性和`length`属性，两者均为`Int`类型。
* 三维坐标系内一点，封装`x`，`y`和`z`属性，三者均为`Double`类型。

在所有其它案例中，定义一个类，生成一个它的实例，并通过引用来管理和传递。实际中，这意味着绝大部分的自定义数据构造都应该是类，而非结构体。

## Day6 2016/08/19

### 属性
#### 存储属性
简单来说，一个存储属性就是存储在特定类或结构体实例里的一个常量或变量。存储属性可以是*变量存储属性*（用关键字`var` 定义），也可以是*常量存储属性*（用关键字 `let` 定义）。
##### 常量结构体的存储属性
如果创建了一个结构体的实例并将其赋值给一个常量，则无法修改该实例的任何属性，即使有属性被声明为变量也不行：

```
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
// 该区间表示整数0，1，2，3
rangeOfFourItems.firstValue = 6
// 尽管 firstValue 是个变量属性，这里还是会报错
```

因为 `rangeOfFourItems` 被声明成了常量（用 `let` 关键字），即使 `firstValue` 是一个变量属性，也无法再修改它了。

这种行为是由于结构体（struct）属于*值类型*。当值类型的实例被声明为常量的时候，它的所有属性也就成了常量。

属于*引用类型*的类（class）则不一样。把一个引用类型的实例赋给一个常量后，仍然可以修改该实例的变量属性。

##### 延迟存储属性

延迟存储属性是指当第一次被调用的时候才会计算其初始值的属性。在属性声明前使用 `lazy` 来标示一个延迟存储属性。

> 注意
> 必须将延迟存储属性声明成变量（使用 `var` 关键字），因为属性的初始值可能在实例构造完成之后才会得到。而常量属性在构造过程完成之前必须要有初始值，因此无法声明成延迟属性。

延迟属性很有用，当属性的值依赖于在实例的构造过程结束后才会知道影响值的外部因素时，或者当获得属性的初始值需要复杂或大量计算时，可以只在需要的时候计算它。

下面的例子使用了延迟存储属性来避免复杂类中不必要的初始化。例子中定义了 `DataImporter` 和 `DataManager` 两个类，下面是部分代码：

```
class DataImporter {
    /*
    DataImporter 是一个负责将外部文件中的数据导入的类。
    这个类的初始化会消耗不少时间。
    */
    var fileName = "data.txt"
    // 这里会提供数据导入功能
}

class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
    // 这里会提供数据管理功能
}

let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// DataImporter 实例的 importer 属性还没有被创建
```

`DataManager` 类包含一个名为 `data` 的存储属性，初始值是一个空的字符串（`String`）数组。这里没有给出全部代码，只需知道 `DataManager` 类的目的是管理和提供对这个字符串数组的访问即可。

`DataManager` 的一个功能是从文件导入数据。该功能由 `DataImporter` 类提供，`DataImporter` 完成初始化需要消耗不少时间：因为它的实例在初始化时可能要打开文件，还要读取文件内容到内存。

`DataManager` 管理数据时也可能不从文件中导入数据。所以当 `DataManager` 的实例被创建时，没必要创建一个`DataImporter` 的实例，更明智的做法是第一次用到 `DataImporter` 的时候才去创建它。

由于使用了 `lazy` ，`importer` 属性只有在第一次被访问的时候才被创建。比如访问它的属性 `fileName` 时：

```
print(manager.importer.fileName)
// DataImporter 实例的 importer 属性现在被创建了
// 输出 "data.txt”
```

> 注意
> 如果一个被标记为 `lazy` 的属性在没有初始化时就同时被多个线程访问，则无法保证该属性只会被初始化一次。

#### 计算属性
除存储属性外，类、结构体和枚举可以定义计算属性。计算属性不直接存储值，而是提供一个 getter 和一个可选的 setter，来间接获取和设置其他属性或变量的值。

```
struct Point {
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
    size: Size(width: 10.0, height: 10.0))
let initialSquareCenter = square.center
square.center = Point(x: 15.0, y: 15.0)
```
`Rect`也提供了一个名为`center` 的计算属性。一个矩形的中心点可以从原点（`origin`）和大小（`size`）算出，所以不需要将它以显式声明的 `Point` 来保存。`Rect` 的计算属性 `center` 提供了自定义的 getter 和 setter 来获取和设置矩形的中心点，就像它有一个存储属性一样。
##### 便捷 setter 声明

如果计算属性的 setter 没有定义表示新值的参数名，则可以使用默认名称 `newValue`。下面是使用了便捷 setter 声明的`Rect` 结构体代码：

```
struct AlternativeRect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }
    }
}
```



##### 只读计算属性

只有 getter 没有 setter 的计算属性就是_只读计算属性_。只读计算属性总是返回一个值，可以通过点运算符访问，但不能设置新的值。

> 注意
> 必须使用 `var` 关键字定义计算属性，包括只读计算属性，因为它们的值不是固定的。`let` 关键字只用来声明常量属性，表示初始化后再也无法修改的值。

只读计算属性的声明可以去掉 `get` 关键字和花括号：

```
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
        return width * height * depth
    }
}
let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
print("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
// 输出 "the volume of fourByFiveByTwo is 40.0"
```

这个例子定义了一个名为 `Cuboid` 的结构体，表示三维空间的立方体，包含 `width`、`height` 和 `depth` 属性。结构体还有一个名为 `volume` 的只读计算属性用来返回立方体的体积。为 `volume` 提供 setter 毫无意义，因为无法确定如何修改 `width`、`height` 和 `depth` 三者的值来匹配新的 `volume`。然而，`Cuboid` 提供一个只读计算属性来让外部用户直接获取体积是很有用的。

#### 属性观察器

_属性观察器_监控和响应属性值的变化，每次属性被设置值的时候都会调用属性观察器，即使新值和当前值相同的时候也不例外。

可以为除了延迟存储属性之外的其他存储属性添加属性观察器，也可以通过重写属性的方式为继承的属性（包括存储属性和计算属性）添加属性观察器。你不必为非重写的计算属性添加属性观察器，因为可以通过它的 setter 直接监控和响应值的变化。 属性重写请参考[重写](http://wiki.jikexueyuan.com/project/swift/chapter2/13_Inheritance.html#overriding)。

可以为属性添加如下的一个或全部观察器：

* `willSet` 在新的值被设置之前调用
* `didSet` 在新的值被设置之后立即调用

`willSet` 观察器会将新的属性值作为常量参数传入，在 `willSet` 的实现代码中可以为这个参数指定一个名称，如果不指定则参数仍然可用，这时使用默认名称 `newValue` 表示。

同样，`didSet` 观察器会将旧的属性值作为参数传入，可以为该参数命名或者使用默认参数名 `oldValue`。如果在`didSet` 方法中再次对该属性赋值，那么新值会覆盖旧的值。

> 注意
> 父类的属性在子类的构造器中被赋值时，它在父类中的 `willSet` 和 `didSet` 观察器会被调用，随后才会调用子类的观察器。在父类初始化方法调用之前，子类给属性赋值时，观察器不会被调用。 有关构造器代理的更多信息，请参考[值类型的构造器代理](http://wiki.jikexueyuan.com/project/swift/chapter2/14_Initialization.html#initializer_delegation_for_value_types)和[类的构造器代理规则](http://wiki.jikexueyuan.com/project/swift/chapter2/14_Initialization.html#initializer_delegation_for_class_types)。

下面是一个 `willSet` 和 `didSet` 实际运用的例子，其中定义了一个名为 `StepCounter` 的类，用来统计一个人步行时的总步数。这个类可以跟计步器或其他日常锻炼的统计装置的输入数据配合使用。

```
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
```

`StepCounter` 类定义了一个 `Int` 类型的属性 `totalSteps`，它是一个存储属性，包含 `willSet` 和 `didSet` 观察器。

当 `totalSteps` 被设置新值的时候，它的 `willSet` 和 `didSet` 观察器都会被调用，即使新值和当前值完全相同时也会被调用。

例子中的 `willSet` 观察器将表示新值的参数自定义为 `newTotalSteps`，这个观察器只是简单的将新的值输出。

`didSet` 观察器在 `totalSteps` 的值改变后被调用，它把新值和旧值进行对比，如果总步数增加了，就输出一个消息表示增加了多少步。`didSet` 没有为旧值提供自定义名称，所以默认值 `oldValue` 表示旧值的参数名。

> 注意
> 
> 如果将属性通过 in-out 方式传入函数，`willSet` 和 `didSet` 也会调用。这是因为 in-out 参数采用了拷入拷出模式：即在函数内部使用的是参数的 copy，函数结束后，又对参数重新赋值。关于 in-out 参数详细的介绍，请参考[输入输出参数](http://wiki.jikexueyuan.com/project/swift/chapter3/05_Declarations.html#in-out_parameters)


#### 类型属性
实例属性属于一个特定类型的实例，每创建一个实例，实例都拥有属于自己的一套属性值，实例之间的属性相互独立。

也可以为类型本身定义属性，无论创建了多少个该类型的实例，这些属性都只有唯一一份。这种属性就是类型属性。

存储型类型属性可以是变量或常量，计算型类型属性跟实例的计算型属性一样只能定义成变量属性。

> 注意
> 跟实例的存储型属性不同，必须给存储型类型属性指定默认值，因为类型本身没有构造器，也就无法在初始化过程中使用构造器给类型属性赋值。
> 存储型类型属性是延迟初始化的，它们只有在第一次被访问的时候才会被初始化。即使它们被多个线程同时访问，系统也保证只会对其进行一次初始化，并且不需要对其使用 `lazy` 修饰符。



##### 类型属性语法

在 C 或 Objective-C 中，与某个类型关联的静态常量和静态变量，是作为全局（_global_）静态变量定义的。但是在 Swift 中，类型属性是作为类型定义的一部分写在类型最外层的花括号内，因此它的作用范围也就在类型支持的范围内。

使用关键字 `static` 来定义类型属性。在为类定义计算型类型属性时，可以改用关键字 `class` 来支持子类对父类的实现进行重写。下面的例子演示了存储型和计算型类型属性的语法：

```
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 1
    }
}
enum SomeEnumeration {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 6
    }
}
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 27
    }
    class var overrideableComputedTypeProperty: Int {
        return 107
    }
}
```

> 注意
> 例子中的计算型类型属性是只读的，但也可以定义可读可写的计算型类型属性，跟计算型实例属性的语法相同。



##### 获取和设置类型属性的值

跟实例属性一样，类型属性也是通过点运算符来访问。但是，类型属性是通过类型本身来访问，而不是通过实例。比如：

```
print(SomeStructure.storedTypeProperty)
// 输出 "Some value."
SomeStructure.storedTypeProperty = "Another value."
print(SomeStructure.storedTypeProperty)
// 输出 "Another value.”
print(SomeEnumeration.computedTypeProperty)
// 输出 "6"
print(SomeClass.computedTypeProperty)
// 输出 "27"
```
## Day7 2016/08/20
### 方法
#### 实例方法 (Instance Methods)

**实例方法**是属于某个特定类、结构体或者枚举类型实例的方法。实例方法提供访问和修改实例属性的方法或提供与实例目的相关的功能，并以此来支撑实例的功能。实例方法的语法与函数完全一致，详情参见[函数](http://wiki.jikexueyuan.com/project/swift/chapter2/06_Functions.html)。

实例方法要写在它所属的类型的前后大括号之间。实例方法能够隐式访问它所属类型的所有的其他实例方法和属性。实例方法只能被它所属的类的某个特定实例调用。实例方法不能脱离于现存的实例而被调用。

下面的例子，定义一个很简单的`Counter`类，`Counter`能被用来对一个动作发生的次数进行计数：

```
class Counter {
    var count = 0
    func increment() {
        count += 1
    }
    func incrementBy(amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}
```

`Counter`类定义了三个实例方法：

* `increment`让计数器按一递增；
* `incrementBy(amount: Int)`让计数器按一个指定的整数值递增；
* `reset`将计数器重置为0。

`Counter`这个类还声明了一个可变属性`count`，用它来保持对当前计数器值的追踪。

和调用属性一样，用点语法（dot syntax）调用实例方法：

```
let counter = Counter()
// 初始计数值是0
counter.increment()
// 计数值现在是1
counter.incrementBy(5)
// 计数值现在是6
counter.reset()
// 计数值现在是0
```



#### 方法的局部参数名称和外部参数名称 (Local and External Parameter Names for Methods)

函数参数可以同时有一个局部名称（在函数体内部使用）和一个外部名称（在调用函数时使用），详情参见[指定外部参数名](http://wiki.jikexueyuan.com/project/swift/chapter2/06_Functions.html#specifying_external_parameter_names)。方法参数也一样（因为方法就是函数，只是这个函数与某个类型相关联了）。

Swift 中的方法和 Objective-C 中的方法极其相似。像在 Objective-C 中一样，Swift 中方法的名称通常用一个介词指向方法的第一个参数，比如：`with`，`for`，`by`等等。前面的`Counter`类的例子中`incrementBy(_:)`方法就是这样的。介词的使用让方法在被调用时能像一个句子一样被解读。

具体来说，Swift 默认仅给方法的第一个参数名称一个局部参数名称；默认同时给第二个和后续的参数名称局部参数名称和外部参数名称。这个约定与典型的命名和调用约定相适应，与你在写 Objective-C 的方法时很相似。这个约定还让富于表达性的方法在调用时不需要再限定参数名称。

看看下面这个`Counter`的另一个版本（它定义了一个更复杂的`incrementBy(_:)`方法）：

```
class Counter {
    var count: Int = 0
    func incrementBy(amount: Int, numberOfTimes: Int) {
        count += amount * numberOfTimes
    }
}
```

`incrementBy(_:numberOfTimes:)`方法有两个参数： `amount`和`numberOfTimes`。默认情况下，Swift 只把`amount`当作一个局部名称，但是把`numberOfTimes`即看作局部名称又看作外部名称。下面调用这个方法：

```
let counter = Counter()
counter.incrementBy(5, numberOfTimes: 3)
// counter 的值现在是 15
```

你不必为第一个参数值再定义一个外部变量名：因为从函数名`incrementBy(_numberOfTimes:)`已经能很清楚地看出它的作用。但是第二个参数，就要被一个外部参数名称所限定，以便在方法被调用时明确它的作用。

上面描述的这种默认行为意味着在 Swift 中，定义方法使用了与 Objective-C 同样的语法风格，并且方法将以自然且富于表达性的方式被调用。


#### self 属性(The self Property)

类型的每一个实例都有一个隐含属性叫做`self`，`self`完全等同于该实例本身。你可以在一个实例的实例方法中使用这个隐含的`self`属性来引用当前实例。

上面例子中的`increment`方法还可以这样写：

```
func increment() {
    self.count += 1
}
```

实际上，你不必在你的代码里面经常写`self`。不论何时，只要在一个方法中使用一个已知的属性或者方法名称，如果你没有明确地写`self`，Swift 假定你是指当前实例的属性或者方法。这种假定在上面的`Counter`中已经示范了：`Counter`中的三个实例方法中都使用的是`count`（而不是`self.count`）。

使用这条规则的主要场景是实例方法的某个参数名称与实例的某个属性名称相同的时候。在这种情况下，参数名称享有优先权，并且在引用属性时必须使用一种更严格的方式。这时你可以使用`self`属性来区分参数名称和属性名称。

下面的例子中，`self`消除方法参数`x`和实例属性`x`之间的歧义：

```
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOfX(x: Double) -> Bool {
        return self.x > x
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOfX(1.0) {
    print("This point is to the right of the line where x == 1.0")
}
// 打印输出: This point is to the right of the line where x == 1.0
```

如果不使用`self`前缀，Swift 就认为两次使用的`x`都指的是名称为`x`的函数参数。

#### 类型方法 (Type Methods)

实例方法是被某个类型的实例调用的方法。你也可以定义在类型本身上调用的方法，这种方法就叫做**类型方法**（Type Methods）。在方法的`func`关键字之前加上关键字`static`，来指定类型方法。类还可以用关键字`class`来允许子类重写父类的方法实现。

> 注意
> 在 Objective-C 中，你只能为 Objective-C 的类类型（classes）定义类型方法（type-level methods）。在 Swift 中，你可以为所有的类、结构体和枚举定义类型方法。每一个类型方法都被它所支持的类型显式包含。

类型方法和实例方法一样用点语法调用。但是，你是在类型上调用这个方法，而不是在实例上调用。下面是如何在`SomeClass`类上调用类型方法的例子：

```
class SomeClass {
    class func someTypeMethod() {
        // type method implementation goes here
    }
}
SomeClass.someTypeMethod()
```

在类型方法的方法体（body）中，`self`指向这个类型本身，而不是类型的某个实例。这意味着你可以用`self`来消除类型属性和类型方法参数之间的歧义（类似于我们在前面处理实例属性和实例方法参数时做的那样）。

一般来说，在类型方法的方法体中，任何未限定的方法和属性名称，可以被本类中其他的类型方法和类型属性引用。一个类型方法可以直接通过类型方法的名称调用本类中的其它类型方法，而无需在方法名称前面加上类型名称。类似地，在结构体和枚举中，也能够直接通过类型属性的名称访问本类中的类型属性，而不需要前面加上类型名称。

### 下标

#### 下标语法

下标允许你通过在实例名称后面的方括号中传入一个或者多个索引值来对实例进行存取。语法类似于实例方法语法和计算型属性语法的混合。与定义实例方法类似，定义下标使用`subscript`关键字，指定一个或多个输入参数和返回类型；与实例方法不同的是，下标可以设定为读写或只读。这种行为由 getter 和 setter 实现，有点类似计算型属性：

```
subscript(index: Int) -> Int {
    get {
      // 返回一个适当的 Int 类型的值
    }

    set(newValue) {
      // 执行适当的赋值操作
    }
}
```

`newValue`的类型和下标的返回类型相同。如同计算型属性，可以不指定 setter 的参数（`newValue`）。如果不指定参数，setter 会提供一个名为`newValue`的默认参数。

如同只读计算型属性，可以省略只读下标的`get`关键字：

```
subscript(index: Int) -> Int {
    // 返回一个适当的 Int 类型的值
}
```

下面代码演示了只读下标的实现，这里定义了一个`TimesTable`结构体，用来表示传入整数的乘法表：

```
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
print("six times three is \(threeTimesTable[6])")
// 输出 "six times three is 18"
```

在上例中，创建了一个`TimesTable`实例，用来表示整数`3`的乘法表。数值`3`被传递给结构体的构造函数，作为实例成员`multiplier`的值。

你可以通过下标访问`threeTimesTable`实例，例如上面演示的`threeTimesTable[6]`。这条语句查询了`3`的乘法表中的第六个元素，返回`3`的`6`倍即`18`。

> 注意
> `TimesTable`例子基于一个固定的数学公式，对`threeTimesTable[someIndex]`进行赋值操作并不合适，因此下标定义为只读的。



#### 下标用法

下标的确切含义取决于使用场景。下标通常作为访问集合（collection），列表（list）或序列（sequence）中元素的快捷方式。你可以针对自己特定的类或结构体的功能来自由地以最恰当的方式实现下标。

例如，Swift 的`Dictionary`类型实现下标用于对其实例中储存的值进行存取操作。为字典设值时，在下标中使用和字典的键类型相同的键，并把一个和字典的值类型相同的值赋给这个下标：

```
var numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
numberOfLegs["bird"] = 2
```

上例定义一个名为`numberOfLegs`的变量，并用一个包含三对键值的字典字面量初始化它。`numberOfLegs`字典的类型被推断为`[String: Int]`。字典创建完成后，该例子通过下标将`String`类型的键`bird`和`Int`类型的值`2`添加到字典中。

### 继承
一个类可以_继承（inherit）_另一个类的方法（methods），属性（properties）和其它特性。当一个类继承其它类时，继承类叫_子类（subclass）_，被继承类叫_超类（或父类，superclass）_。在 Swift 中，继承是区分「类」与其它类型的一个基本特征。

在 Swift 中，类可以调用和访问超类的方法，属性和下标（subscripts），并且可以重写（override）这些方法，属性和下标来优化或修改它们的行为。Swift 会检查你的重写定义在超类中是否有匹配的定义，以此确保你的重写行为是正确的。

可以为类中继承来的属性添加属性观察器（property observers），这样一来，当属性值改变时，类就会被通知到。可以为任何属性添加属性观察器，无论它原本被定义为存储型属性（stored property）还是计算型属性（computed property）。



#### 定义一个基类（Defining a Base Class）

不继承于其它类的类，称之为_基类（base class）_。

> 注意
> Swift 中的类并不是从一个通用的基类继承而来。如果你不为你定义的类指定一个超类的话，这个类就自动成为基类。

下面的例子定义了一个叫`Vehicle`的基类。这个基类声明了一个名为`currentSpeed`，默认值是`0.0`的存储属性（属性类型推断为`Double`）。`currentSpeed`属性的值被一个`String`类型的只读计算型属性`description`使用，用来创建车辆的描述。

`Vehicle`基类也定义了一个名为`makeNoise`的方法。这个方法实际上不为`Vehicle`实例做任何事，但之后将会被`Vehicle`的子类定制：

```
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    func makeNoise() {
        // 什么也不做-因为车辆不一定会有噪音
    }
}
```

您可以用初始化语法创建一个`Vehicle`的新实例，即类名后面跟一个空括号：

```
let someVehicle = Vehicle()
```

现在已经创建了一个`Vehicle`的新实例，你可以访问它的`description`属性来打印车辆的当前速度：

```
print("Vehicle: \(someVehicle.description)")
// Vehicle: traveling at 0.0 miles per hour
```

`Vehicle`类定义了一个通用特性的车辆类，实际上没什么用处。为了让它变得更加有用，需要完善它从而能够描述一个更加具体类型的车辆。



#### 子类生成（Subclassing）

_子类生成（Subclassing）_指的是在一个已有类的基础上创建一个新的类。子类继承超类的特性，并且可以进一步完善。你还可以为子类添加新的特性。

为了指明某个类的超类，将超类名写在子类名的后面，用冒号分隔：

```
class SomeClass: SomeSuperclass {
    // 这里是子类的定义
}
```

下一个例子，定义一个叫`Bicycle`的子类，继承成父类`Vehicle`：

```
class Bicycle: Vehicle {
    var hasBasket = false
}
```

新的`Bicycle`类自动获得`Vehicle`类的所有特性，比如`currentSpeed`和`description`属性，还有它的`makeNoise()`方法。

除了它所继承的特性，`Bicycle`类还定义了一个默认值为`false`的存储型属性`hasBasket`（属性推断为`Bool`）。

默认情况下，你创建任何新的`Bicycle`实例将不会有一个篮子（即`hasBasket`属性默认为`false`），创建该实例之后，你可以为特定的`Bicycle`实例设置`hasBasket`属性为`ture`：

```
let bicycle = Bicycle()
bicycle.hasBasket = true
```

你还可以修改`Bicycle`实例所继承的`currentSpeed`属性，和查询实例所继承的`description`属性：

```
bicycle.currentSpeed = 15.0
print("Bicycle: \(bicycle.description)")
// Bicycle: traveling at 15.0 miles per hour
```

子类还可以继续被其它类继承，下面的示例为`Bicycle`创建了一个名为`Tandem`（双人自行车）的子类：

```
class Tandem: Bicycle {
    var currentNumberOfPassengers = 0
}
```

`Tandem`从`Bicycle`继承了所有的属性与方法，这又使它同时继承了`Vehicle`的所有属性与方法。`Tandem`也增加了一个新的叫做`currentNumberOfPassengers`的存储型属性，默认值为`0`。

如果你创建了一个`Tandem`的实例，你可以使用它所有的新属性和继承的属性，还能查询从`Vehicle`继承来的只读属性`description`：

```
let tandem = Tandem()
tandem.hasBasket = true
tandem.currentNumberOfPassengers = 2
tandem.currentSpeed = 22.0
print("Tandem: \(tandem.description)")
// Tandem: traveling at 22.0 miles per hour
```



#### 重写（Overriding）

子类可以为继承来的实例方法（instance method），类方法（class method），实例属性（instance property），或下标（subscript）提供自己定制的实现（implementation）。我们把这种行为叫_重写（overriding）_。

如果要重写某个特性，你需要在重写定义的前面加上`override`关键字。这么做，你就表明了你是想提供一个重写版本，而非错误地提供了一个相同的定义。意外的重写行为可能会导致不可预知的错误，任何缺少`override`关键字的重写都会在编译时被诊断为错误。

`override`关键字会提醒 Swift 编译器去检查该类的超类（或其中一个父类）是否有匹配重写版本的声明。这个检查可以确保你的重写定义是正确的。

##### 访问超类的方法，属性及下标

当你在子类中重写超类的方法，属性或下标时，有时在你的重写版本中使用已经存在的超类实现会大有裨益。比如，你可以完善已有实现的行为，或在一个继承来的变量中存储一个修改过的值。

在合适的地方，你可以通过使用`super`前缀来访问超类版本的方法，属性或下标：

* 在方法`someMethod()`的重写实现中，可以通过`super.someMethod()`来调用超类版本的`someMethod()`方法。
* 在属性`someProperty`的 getter 或 setter 的重写实现中，可以通过`super.someProperty`来访问超类版本的`someProperty`属性。
* 在下标的重写实现中，可以通过`super[someIndex]`来访问超类版本中的相同下标。

##### 重写方法

在子类中，你可以重写继承来的实例方法或类方法，提供一个定制或替代的方法实现。

下面的例子定义了`Vehicle`的一个新的子类，叫`Train`，它重写了从`Vehicle`类继承来的`makeNoise()`方法：

```
class Train: Vehicle {
    override func makeNoise() {
        print("Choo Choo")
    }
}
```

如果你创建一个`Train`的新实例，并调用了它的`makeNoise()`方法，你就会发现`Train`版本的方法被调用：

```
let train = Train()
train.makeNoise()
// 打印 "Choo Choo"
```

##### 重写属性

你可以重写继承来的实例属性或类型属性，提供自己定制的 getter 和 setter，或添加属性观察器使重写的属性可以观察属性值什么时候发生改变。

###### 重写属性的 Getters 和 Setters

你可以提供定制的 getter（或 setter）来重写任意继承来的属性，无论继承来的属性是存储型的还是计算型的属性。子类并不知道继承来的属性是存储型的还是计算型的，它只知道继承来的属性会有一个名字和类型。你在重写一个属性时，必需将它的名字和类型都写出来。这样才能使编译器去检查你重写的属性是与超类中同名同类型的属性相匹配的。

你可以将一个继承来的只读属性重写为一个读写属性，只需要在重写版本的属性里提供 getter 和 setter 即可。但是，你不可以将一个继承来的读写属性重写为一个只读属性。

> 注意
> 如果你在重写属性中提供了 setter，那么你也一定要提供 getter。如果你不想在重写版本中的 getter 里修改继承来的属性值，你可以直接通过`super.someProperty`来返回继承来的值，其中`someProperty`是你要重写的属性的名字。

以下的例子定义了一个新类，叫`Car`，它是`Vehicle`的子类。这个类引入了一个新的存储型属性叫做`gear`，默认值为整数`1`。`Car`类重写了继承自`Vehicle`的`description`属性，提供包含当前档位的自定义描述：

```
class Car: Vehicle {
    var gear = 1
    override var description: String {
        return super.description + " in gear \(gear)"
    }
}
```

重写的`description`属性首先要调用`super.description`返回`Vehicle`类的`description`属性。之后，`Car`类版本的`description`在末尾增加了一些额外的文本来提供关于当前档位的信息。

如果你创建了`Car`的实例并且设置了它的`gear`和`currentSpeed`属性，你可以看到它的`description`返回了`Car`中的自定义描述：

```
let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("Car: \(car.description)")
// Car: traveling at 25.0 miles per hour in gear 3
```



###### 重写属性观察器（Property Observer）

你可以通过重写属性为一个继承来的属性添加属性观察器。这样一来，当继承来的属性值发生改变时，你就会被通知到，无论那个属性原本是如何实现的。关于属性观察器的更多内容，请看[属性观察器](http://wiki.jikexueyuan.com/project/swift/chapter2/10_Properties.html#property_observers)。

> 注意
> 你不可以为继承来的常量存储型属性或继承来的只读计算型属性添加属性观察器。这些属性的值是不可以被设置的，所以，为它们提供`willSet`或`didSet`实现是不恰当。
> 此外还要注意，你不可以同时提供重写的 setter 和重写的属性观察器。如果你想观察属性值的变化，并且你已经为那个属性提供了定制的 setter，那么你在 setter 中就可以观察到任何值变化了。

下面的例子定义了一个新类叫`AutomaticCar`，它是`Car`的子类。`AutomaticCar`表示自动挡汽车，它可以根据当前的速度自动选择合适的挡位:

```
class AutomaticCar: Car {
    override var currentSpeed: Double {
        didSet {
            gear = Int(currentSpeed / 10.0) + 1
        }
    }
}
```

当你设置`AutomaticCar`的`currentSpeed`属性，属性的`didSet`观察器就会自动地设置`gear`属性，为新的速度选择一个合适的挡位。具体来说就是，属性观察器将新的速度值除以`10`，然后向下取得最接近的整数值，最后加`1`来得到档位`gear`的值。例如，速度为`35.0`时，挡位为`4`：

```
let automatic = AutomaticCar()
automatic.currentSpeed = 35.0
print("AutomaticCar: \(automatic.description)")
// AutomaticCar: traveling at 35.0 miles per hour in gear 4
```



#### 防止重写

你可以通过把方法，属性或下标标记为_`final`_来防止它们被重写，只需要在声明关键字前加上`final`修饰符即可（例如：`final var`，`final func`，`final class func`，以及`final subscript`）。

如果你重写了带有`final`标记的方法，属性或下标，在编译时会报错。在类扩展中的方法，属性或下标也可以在扩展的定义里标记为 final 的。

你可以通过在关键字`class`前添加`final`修饰符（`final class`）来将整个类标记为 final 的。这样的类是不可被继承的，试图继承这样的类会导致编译报错。

