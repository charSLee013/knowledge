# Golang

- [Golang](#golang)
  - [下面Go程序的输出结果为()](#下面go程序的输出结果为)
  - [下面golang程序的执行结果是()](#下面golang程序的执行结果是)
  - [Go语言默认的编码格式是()](#go语言默认的编码格式是)
  - [下面Golang程序的输出结果为()](#下面golang程序的输出结果为)
  - [在Go语言中，下面能表示"coderA\>1 并且 coderA\<10"的表达式是（）](#在go语言中下面能表示codera1-并且-codera10的表达式是)
  - [下面Golang程序的输出结果为()](#下面golang程序的输出结果为-1)
  - [有下面Golang程序，在横线部分填入下面哪个选项可以使程序正确运行（）](#有下面golang程序在横线部分填入下面哪个选项可以使程序正确运行)


## 下面Go程序的输出结果为()
```golang
package main

import (
    "fmt"
)

func main(){
    fmt.Printf("%%%")
}
```

A. %

B. %%

C. 编译错误

D. %%%

<details close>
<summary>答案解析</summary>

这个程序会产生编译错误，因为`fmt.Printf`函数的第一个参数是一个格式化字符串，它需要包含一个或多个占位符，如`%d`, `%s`, ``%f``等，来表示后面的参数的类型和位置。

而这个程序中的格式化字符串只有三个百分号，没有任何占位符，所以编译器会报错，说缺少参数。如果想要输出百分号，需要用两个百分号来表示一个百分号，如`fmt.Printf("%%")`会输出`%`。其他选项都不是正确的输出结果。
</details open>

## 下面golang程序的执行结果是()

```golang
package main

import "fmt"

type CoderCounter struct {
    CardNO string `json:"card_no"`
    RealName string `json:"real_name"`
    Total int64 `json:"total"`
}

type Option func(*CoderCounter)

func WithCardNO(cardNO string) Option {
    return func(u *CoderCounter){
        u.CardNO = cardNO
    }   
}

func WithTotal(total int64) Option {
    return func(u *CoderCounter){
        u.Total = total
    }
}

func WithRealName(realName string) Option {
    return func(u *CoderCounter){
        u.RealName  = realname
    }
}

func DefaultCoderCounter() CoderCounter {
    return CoderCounter {
        CardNO:  "612828***1998",
        RealName: "张三",
        Total: 1,
    }
}

func NewCoderCounter(ops ...func(*CoderCounter))(*CoderCounter, error){
    counter := DefaultCoderCounter()
    for _,op := range ops {
        op(&counter)
    }
    return &counter,nil
}

func main(){
    coderCounter,_ := NewCoderCounter(WithCardNO("123456789"),WithTotal(99))
    fmt.Println(*coderCounter)
    return
}
```

A. {612828***1998 张三 1}

B. {612828***1998 张三 99}

C. {123456789 张三 99}

D. {123456789 张三 1}

<details close>
<summary>答案解析</summary>

这个程序定义了一个`CoderCounter`结构体，它有三个字段：`CardNO`, `RealName`, `Total`。

然后定义了三个`Option`类型的函数，它们分别用来修改`CoderCounter`的`CardNO`, `RealName`, `Total`字段。
接着定义了一个DefaultCoderCounter函数，它返回一个CoderCounter结构体的值，它的字段是默认的。
最后定义了一个NewCoderCounter函数，它接受一个可变参数ops，它是Option类型的函数的切片，然后对每个ops中的函数，都调用它，并传入DefaultCoderCounter返回的结构体的地址，这样就可以修改结构体的字段。

在main函数中，调用了`NewCoderCounter`函数，并传入了两个Option类型的函数：`WithCardNO("123456789")`和`WithTotal(99)`，它们分别修改了结构体的CardNO和Total字段。然后打印出coderCounter指针指向的结构体的值，结果是{123456789 张三 99}。

其他选项都不是正确的执行结果。所以选择 C
</details>


## Go语言默认的编码格式是()

A. GBK

B. UTF-8

C. ASCII

D. Unicode

<details close>
<summary>答案解析</summary>

Go语言默认的编码格式是`UTF-8`，它是一种兼容ASCII的可变长度的编码方式，它可以表示世界上几乎所有的语言字符。
GBK是一种中文编码方式，它不是Go语言的默认编码格式。ASCII是一种单字节的编码方式，它只能表示128个字符，它不够用来表示Go语言的源代码。Unicode是一种字符集，它定义了每个字符的唯一编号，但它不是一种编码方式，它需要和UTF-8等编码方式配合使用。

所以选择B
</details>


## 下面Golang程序的输出结果为()

```golang
package main

import "fmt"

func hello(i int){
    fmt.Println(i)
}

func main(){
    i := 5
    defer hello(i)
    i = i + 10
}

```

A. 5

B. 10

C. 编译错误

D. 15


<details close>
<summary>答案解析</summary>
这个程序使用了defer关键字，它可以延迟一个函数的执行，直到包含它的函数返回。
在main函数中，调用了defer hello(i)，它会把i的值作为参数传给hello函数，但是不会立即执行hello函数，而是等到main函数结束后再执行。
如果将代码进行反编译的话，就会得到如下伪代码

```golang
var i int = 5
var a int = i   // 此处记录defer所需参数

i = i + 10

// 在return 之前按照FILO规则执行 defer
hello(a)

return
```

然后，i的值被加上了10，变成了15，但是这个改变不会影响到defer hello(i)中的i的值，因为它已经被传递了。
所以，当main函数返回时，会执行hello函数，并打印出i的值，即5。其他选项都不是正确的输出结果。
</details>


## 在Go语言中，下面能表示"coderA>1 并且 coderA<10"的表达式是（）

A. coderA > 1 & coderA < 10

B. coderA > 1 | coderA < 10

C. coderA > 1 && coderA < 10

D. coder A > 1 || coderA < 10


<details close>
<summary>答案解析</summary>
在Go语言中，表示逻辑与的运算符是&&，表示逻辑或的运算符是||，而&和|是位运算符，它们对两个整数的每一位进行与或运算。所以，要表示"coderA>1 并且 coderA<10"，需要用coderA > 1 && coderA < 10

所以选择 C

</details>


## 下面Golang程序的输出结果为()

```golang
package main

import "fmt"

func main(){
    s := make(map[string]int)
    delete(s,"h")
    fmt.Println(s["h"])
}
```

A. 0

B. 1

C. 运行错误

D. 编译错误


<details close>
<summary>答案解析</summary>
这个程序创建了一个空的map，它的键是字符串类型，值是整数类型。
然后调用了delete函数，删除了键为"h"的元素，但是因为这个map本来就是空的，所以这个操作没有任何效果。
接着打印出了s["h"]的值，因为这个键不存在于map中，所以会返回值类型的零值，即0。其他选项都不是正确的输出结果。
</details>

## 有下面Golang程序，在横线部分填入下面哪个选项可以使程序正确运行（）

```golang
package main

import (
    "encoding/json"
    "fmt"
)

func main(){
    coderCh := make(chan bool, 1)
    go func(coderCh chan bool){
        var (
            coderCode = `{"result_code":9999}`
            coderResult = make(map[string]interface{},10)
        )
        err := json.Unmarshal([]byte(coderCode),&coderResult)
        if err != nil {
            fmt.Println("json.Unmarshal error:",err,coderCode)
            return
        }

        ______________________________________
        fmt.Println("marshalData value info: ",marshaData)
        coderCh <- true
    }(coderCh)

    <-coderCh
    return
}
```

A. `marshalData := coderResult["result_code"].(float32)

B. `marshalData := coderResult["result_code"].(float64)

C. `marshalData := coderResult["result_code"].(int64)

D. `marshalData := coderResult["result_code"].(int32)


<details close>
<summary>答案解析</summary>

这个程序使用了`json.Unmarshal`函数，它可以把一个JSON格式的字符串转换成一个Go语言的值，存储在coderResult这个map中。

但是，因为coderResult的值类型是interface{}，它可以表示任何类型的值，所以需要用类型断言来获取具体的类型和值。

在这个程序中，coderCode中的result_code的值是9999，它是一个整数，但是**在JSON中，所有的数字都是浮点数**，所以json.Unmarshal函数会把它转换成float64类型的值。

所以，在横线部分，需要用marshalData := coderResult["result_code"].(float64)这个表达式，来获取result_code对应的**float64类型的值**，并赋值给marshalData变量。然后打印出marshalData的值，结果是9999。其他选项都不是正确的类型断言，它们会导致运行时错误。

所以选择 B
</details>

