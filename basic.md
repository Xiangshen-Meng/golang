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
