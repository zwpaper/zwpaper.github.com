---
title: 擦肩而过的 Golang Channel Bug
tags: 
- Golang
- Tech
---

nil channel 是可以读写的
只是会阻塞

https://groups.google.com/forum/#!topic/golang-nuts/QltQ0nd9HvE

只有出现死锁的时候，才会报错

Receiving from a nil channel blocks forever. A receive operation on a closed channel can always proceed immediately, yielding the element type's zero value after any previously sent values have been received.
https://golang.org/ref/spec#Receive_operator

A send on a nil channel blocks forever.

两个返回值方式读一个 closed chan，可以判断chan是不是已经关闭

    case _, ok := <-ch2:
        if !ok {
            isClosed2 = true

linux amd64
1.7.2，1.6.2 
```
package main

import "fmt"

func main() {
        var ch chan struct{}
        fmt.Println("Before read chan")
        <-ch
        fmt.Println("after read chan")
}
```

```
Before read chan
fatal error: all goroutines are asleep - deadlock!

goroutine 1 [chan receive (nil chan)]:
main.main()
        /home/zhangwei/go_test/chan_bug/chan_bug.go:8 +0xc1
exit status 2
```


```
func main() {
        var ch chan struct{}
        go func(){
                fmt.Println("Before read in go routine")
                time.Sleep(time.Second*10)
                <-ch
                fmt.Println("After read in go routine")
        }()
        fmt.Println("Before read chan")
        <-ch
        fmt.Println("after read chan")
}
```


```
Before read chan
Before read in go routine
```
过了 10 秒钟
```
fatal error: all goroutines are asleep - deadlock!

goroutine 1 [chan receive (nil chan)]:
main.main()
        /tmp/main.go:17 +0x12b

goroutine 5 [chan receive (nil chan)]:
main.main.func1(0x0)
        /tmp/main.go:13 +0x117
created by main.main
        /tmp/main.go:15 +0x43
exit status 2
```

