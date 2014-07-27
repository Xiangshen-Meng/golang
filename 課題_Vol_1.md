### 課題１
（初心者向け）

Golangで「消費者と生産者」の問題を実現しよう！

[消費者と生産者問題の参考](http://www.weblio.jp/wkpja/content/%E3%82%BB%E3%83%9E%E3%83%95%E3%82%A9_%E4%BE%8B%3A+%E7%94%9F%E7%94%A3%E8%80%85/%E6%B6%88%E8%B2%BB%E8%80%85%E5%95%8F%E9%A1%8C)
```go
package main
 
import "fmt"
import "time"
 
var done = make(chan bool)
var msgs = make(chan int, 3)
 
func produce () {
  for i := 0; i < 100; i++ {
    msgs <- i
    fmt.Println("Produce : ", i)
    time.Sleep(time.Second)
  }
  done <- true
}
 
func consume () {
  for {
    msg := <-msgs
    fmt.Println("Consume : ", msg)
    time.Sleep(2*time.Second)
  }
}
 
func main () {
  go produce()
  go consume()
  <- done
}
```
### 課題２
（初心者向け）

GolangでJsonを分析しよう！
（json内容がありませんでしたら、connpass APIを使いましょう）

[Json](https://gobyexample.com/json)

[net/http](http://golang.org/pkg/net/http/)

### 課題３
（中級向け）

web applicationのHello worldを立ち上げましょう！

（申し訳ございません、私もできません、Golangでweb serviceを作り方、どうぞ）

### 課題４
（中級向け）

GolangでSSHを通じて、リモートのサーバを操作しよう！（自分はこれをチャレンジしたい）

[SSHパッケージの参考](https://godoc.org/code.google.com/p/go.crypto/ssh)

[SSHの例](http://kukuruku.co/hub/golang/ssh-commands-execution-on-hundreds-of-servers-via-go)

### 課題５

（高級向け）

* cockroach
* kubernetes
* cayley
* docker

ソースコードを勉強したい方、どうぞ（私もできません。(T_T)）

