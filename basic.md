### 基本知識
#### Hello World
```go
package main
import "fmt"

func main() {
  fmt.Println("hello world")
}
```

#### 変数 & タイプ
```go
package main
import "fmt"

func main() {
  var a string = "Hello World"
  //a := "Hello World"
  fmt.Println(a)
  
  var b, c int = 1, 2
  fmt.Println(b, c)
  
  arr := [5]int{1, 2, 3, 4, 5}
  fmt.Println(arr)
  
  sarr := make([]string, 3)
  
  sarr[0] = "a"
  sarr[1] = "b"
  sarr[2] = "c"
  fmt.Println(sarr)
  
  sarr = append(s, "d")
  sarr = append(s, "e", "f")
  fmt.Println(sarr)
  
  js := map[string]string{}
  //js := make(map[string]string)
  js["name"] = "Golang"
  js["birthday"] = "2009"
  fmt.Println(js)

  mjson := map[string]interface{}{}
  mjson["name"] = "Let's Go !"
  mjson["birthday"] = 201407
  fmt.Printf("%#v", mjson)
}
```
[Array & Slice](http://blog.golang.org/go-slices-usage-and-internals)

#### IF / For
```go
package main
import "fmt"

func main() {
  js := map[string]string{}
  js["name"] = "Golang"
  js["birthday"] = "2009"
  
  for i := 0; i <= 9; i++ {
    fmt.Println(i)
  }
  
  b := true
  if b {
    fmt.Println("It's true")
  }
  
  if v, has := js["name"]; has {
    fmt.Println(v)
  }
  
  if v, has := js["na"]; has {
    fmt.Println(v)
  }
  
  for k, v := range js {
    fmt.Println("key:", k)
    fmt.Println("value:", v)
  }
}
```

#### メソッド
```go
package main
import "fmt"

func plusab(a, b int) (int, string) {
  return a+b, "OK"
}

func main() {
  res, s := plusab(1, 3)
  fmt.Println(res, s)
}
```
```go
package main
import "fmt"

func printjson(j map[string]interface{}) {
  for k, v := range j {
    if val, ok := v.(string); ok {
      fmt.Println("Key:", k, " Value:", val)
    }
  }
}

func main() {

  mjson := map[string]interface{}{}
  mjson["name"] = "Let's Go !"
  mjson["birthday"] = 201407
  fmt.Printf("%#v\n", mjson)

  printjson(mjson)
}
```

```go
package main
import "fmt"

func printjson(j map[string]interface{}) {
  for _, v := range j {
    switch v := v.(type) {
      default:
        fmt.Println("Default")
      case string:
        fmt.Println("It's string ", v)
      case int:
        fmt.Println("It's int ", v)
    }
  }
}

func main() {

  mjson := map[string]interface{}{}
  mjson["name"] = "Let's Go !"
  mjson["birthday"] = 201407
  fmt.Printf("%#v\n", mjson)

  printjson(mjson)
}
```
#### interface & struct
```go
package main

import "fmt"
import "math"

type geometry interface {
    area() float64
    perim() float64
}

type square struct {
    width, height float64
}
type circle struct {
    radius float64
}

func (s square) area() float64 {
    return s.width * s.height
}
func (s square) perim() float64 {
    return 2*s.width + 2*s.height
}

func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perim() float64 {
    return 2 * math.Pi * c.radius
}

func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}

func main() {
    s := square{width: 3, height: 4}
    c := circle{radius: 5}

    measure(s)
    measure(c)
}
```
#### goroutine & channel
```go
package main

import "fmt"
import "time"

func f(from string) {
    for i := 0; i < 3; i++ {
        time.Sleep(1000 * time.Millisecond)
        fmt.Println(from, ":", i)
    }
}

func main() {

    f("direct")
    go f("goroutine")
    go func(msg string) {
        fmt.Println(msg)
    }("going")

    var input string
    fmt.Scanln(&input)
    fmt.Println("done")
}
```
```go
package main

import "fmt"

func main() {

    messages := make(chan string)
    go func() { messages <- "ping" }()

    msg := <-messages
    fmt.Println(msg)
}
```
```go
package main

import (
  "fmt"
  "time"
)

func pinger(c chan string) {
  for i := 0; ; i++ {
    c <- "ping"
  }
}

func printer(c chan string) {
  for {
    msg := <- c
    fmt.Println(msg)
    time.Sleep(time.Second * 1)
  }
}

func main() {
  var c chan string = make(chan string)

  go pinger(c)
  go printer(c)

  var input string
  fmt.Scanln(&input)
}
```
```go
package main

import "fmt"
import "time"

func main() {
  c1 := make(chan string)
  c2 := make(chan string)

  go func() {
    for {
      c1 <- "from 1"
      time.Sleep(time.Second * 2)
    }
  }()
  go func() {
    for {
      c2 <- "from 2"
      time.Sleep(time.Second * 3)
    }
  }()
  go func() {
    for {
      select {
        case msg1 := <-c1:
          fmt.Println(msg1)
        case msg2 := <-c2:
          fmt.Println(msg2)
        case <- time.After(time.Second):
          fmt.Println("timeout")
      }
    }
  }()

  var input string
  fmt.Scanln(&input)
}
```
