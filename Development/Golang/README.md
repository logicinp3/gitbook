---
icon: code
description: Golang training
---

# Golang

## 1. Development Environment

### Install
```bash
# Download and Install
# https://go.dev/doc/install

# Managing Go installations
# https://go.dev/doc/manage-install

# Installing from source
# https://go.dev/doc/install/source
```

### Goland
```bash
# active
cat ./ideaActive/ja-netfilter-all/ja-netfilter/readme.txt

# plugins
gradianto # themes
rainbow brackets # json
```

## 2. ProjectManage

```bash
go mod init go-example

go mod tidy

go mod vendor
```


## 3. Training

### Basic grammar

#### Commentary

```go
/*
Go programs doc.

Usage:

    gofmt [flags] [path ...]

The flags are:

    -x xxx
    -y yyy
*/
package main
import "fmt"

func main() {
    fmt.Println("hello world!") // Oneline comment

}
// go doc tmp.go
```

#### Constants
```go
type ByteSize float64

const (
    _           = iota // ignore first value by assigning to blank identifier
    KB ByteSize = 1 << (10 * iota)
    MB
    GB
    TB
    PB
    EB
    ZB
    YB
)
func (b ByteSize) String() string {
    switch {
    case b >= YB:
        return fmt.Sprintf("%.2fYB", b/YB)
    case b >= ZB:
        return fmt.Sprintf("%.2fZB", b/ZB)
    case b >= EB:
        return fmt.Sprintf("%.2fEB", b/EB)
    case b >= PB:
        return fmt.Sprintf("%.2fPB", b/PB)
    case b >= TB:
        return fmt.Sprintf("%.2fTB", b/TB)
    case b >= GB:
        return fmt.Sprintf("%.2fGB", b/GB)
    case b >= MB:
        return fmt.Sprintf("%.2fMB", b/MB)
    case b >= KB:
        return fmt.Sprintf("%.2fKB", b/KB)
    }
    return fmt.Sprintf("%.2fB", b)
}
```

#### Variables
```go
// option1
var (
    x string
    y int
)
x,y = "a",2
// option2
var x,y = "a",2
// option3
x,y := "a",2

// anonymous variable
_, _ = call_function()
```

#### Operator
```go
// arithmetic
+
-
*
/
%

// relational
x == x
x != x
>
<
>=
<=

// logical
x && y
x || y
!(x < 18)

// assignment
x = 1
x += 1
x -= 1
x *= 1
x /= 1
x %= 1
x <= 1
x >= 1
x &= 1
x ^= 1
x |= 1
```


#### Printing and Formatting

```go
package main
import "fmt"

func main() {
    // Print, Println
    fmt.Print("xxx")
    fmt.Println("yyy")

    var name string = "aaa"
    var age int = 33
    var height float64 = 1.1
    var p *string = &name
    // Printf, Sprintf
    fmt.Printf("%s %d %f %p %b", name, age, height, p, age)
    s := fmt.Sprintf("%s %d %f %p %b", name, age, height, p, age)
    fmt.Println(s)

    var (
        name     string
        age      int
        married  bool
    )
    // Scan, Scanf, Scanln
    fmt.Scan(&name, &age, &married)
    fmt.Scanf("1:%s 2:%d 3:%t", &name, &age, &married)
    fmt.Scanln(&name, &age, &married)
    //
    fmt.Printf("name:%s age:%d married:%t", name, age, married)

}
```

### Data type

#### bool
```go
var b1 = true
var b2 = false
fmt.Println(reflect.TypeOf(b1), reflect.TypeOf(b2))
```

#### float
```go
var f1 float32 = 3.1234567890123456789
f1 = 2e10
fmt.Println(f1, reflect.TypeOf(f1))

var f2 float64 = 3.1234567890123456789
f2 = 2e-2
fmt.Println(f2, reflect.TypeOf(f2))
```

#### int
```go
/*  
    int8	-128~127
    uint8	0~255
    int16	-32768~32767
    uint16	0~65535
    int32	-2147483648~2147483647
    uint32	0~4294967295
    int64	-9223372036854775808~9223372036854775807
    uint64	0~18446744073709551615
    uint	32-bit operating system is uint32,64-bit operating system is uint64
    int     32-bit operating system is int32,64-bit operating system is int64
*/
var i int = 10
fmt.Printf("%d \n", i)  // 10
fmt.Printf("%b \n", i)  // 1010
fmt.Printf("%o \n", i)  // 12
fmt.Printf("%x \n", i)  // a
```

#### string
```go
/*  
    \r	回车符（返回行首）
    \n	换行符（直接跳到下一行的同列位置）
    \t	制表符
    \'	单引号
    \"	双引号
    \\	反斜杠
*/
var s string = "hello world"
s1 := s[1:3]
s2 := string(s[0]) + string(s[4])
s3 := `
multi line one
multi line two
`
fmt.Println(s1, s2, s3)


// strings method
fmt.Println(strings.ToUpper(s))
fmt.Println(strings.ToLower(s))
fmt.Println(strings.TrimLeft(s, ""))
fmt.Println(strings.Trim(s, ""))
fmt.Println(strings.Index(s, "world"))
fmt.Println(strings.HasPrefix(s, "hello"))
fmt.Println(strings.Contains(s, "llo"))
fmt.Println(strings.Join([]string{"a","b","c"}, ","))

// strconv method
// int to int
i = 100
fmt.Println(int64(i), reflect.TypeOf(int64(i)))
fmt.Println(float64(i), reflect.TypeOf(float64(i)))
// int to string
x := strconv.Itoa(98)
fmt.Println(x, reflect.TypeOf(x))
// string to int
y, _ := strconv.Atoi("97")
fmt.Println(y, reflect.TypeOf(y))
i1, _ := strconv.ParseInt("1000", 10, 8)
println(i1)
i2, _ := strconv.ParseInt("1000", 10, 64)
println(i2)
// string to float
f2, _ := strconv.ParseFloat("3.1415926", 64)
fmt.Println(f2, reflect.TypeOf(f2))
f1, _ := strconv.ParseFloat("3.1415926", 32)
fmt.Println(f1, reflect.TypeOf(f1))
// string to bool
b1, _ := strconv.ParseBool("true")
fmt.Println(b1, reflect.TypeOf(b1))
b2, _ := strconv.ParseBool("T")
fmt.Println(b2, reflect.TypeOf(b2))
b3, _ := strconv.ParseBool("1")
fmt.Println(b3, reflect.TypeOf(b3))
b4, _ := strconv.ParseBool("100")
fmt.Println(b4, reflect.TypeOf(b4))
```

#### Arrays
```go
var arr [3]int8 = [3]int8{1,2,3}
//var arr [3]int = [3]int{1,2,3}
fmt.Printf("%p\n", &arr)
fmt.Println(&arr[0])
fmt.Println(&arr[1])
fmt.Println(&arr[2])
```

#### Slices

#### Maps


### Control structures

#### if
```go
// if
if true {
    // do something
}

// if, else
score := 33
if score < 10 {
    fmt.Println("less than 10")
} else {
    fmt.Println("greater than 10")
}

// if, else if, else
if score < 10 {
    fmt.Println("less than 10")
} else if score < 20 {
    fmt.Println("less than 20")
} else {
    fmt.Println("greater than 20")
}
```

#### switch
```go
choice := "fff"
switch choice {
    case "a":
        fmt.Println("a")
    case "b":
        fmt.Println("b")
    case "x", "y":
        fmt.Println("xy")
    default:
        fmt.Println("x")
}
```

#### for
```go
count := 0
for count < 10 {
    fmt.Println(count)
    // count ++
    count += 1
}

for i:=1; i<10; i++ {
    if i % 2 == 0{
        fmt.Println(i)
    } else if i == 7 {
        // continue
        break
    }
}

var names [3]int = [3]int{1,2,3}
var names = [...]string{"a","b","c"}
for k,v := range names {
    fmt.Println(k,v)
}
```




### Functions

#### Defer


### Data

#### Allocation with new

```go
var p *int = new(int)
fmt.Println(*p)
```

#### Allocation with make

```go
var s []int = make([]int, 3, 5)
//var s []string = make([]string, 3, 5)
fmt.Println(s)
```






### The init function
```go
func init() {
    if user == "" {
        log.Fatal("$USER not set")
    }
    if home == "" {
        home = "/home/" + user
    }
    if gopath == "" {
        gopath = home + "/go"
    }
    // gopath may be overridden by --gopath flag on command line.
    flag.StringVar(&gopath, "gopath", gopath, "override default GOPATH")
}
```


## Methods

### Pointers vs. Values

```go
var x int = 10
fmt.Printf("%p\n", &x)
var p *int = &x
fmt.Printf("%p\n", &p)
fmt.Println(p)
fmt.Println(*p)
```

## Interfaces and other types

### Interfaces

### Conversions

### Interface conversions and type assertions

### Generality

### Interfaces and methods


> Reference:
> 1. [Official Website](https://go.dev)
> 2. [Repository](https://github.com/golang/go)
> 3. [Go语言中文网](https://studygolang.com/dl)
