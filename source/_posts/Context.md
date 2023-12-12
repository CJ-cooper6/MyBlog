---
title: Context
---

上下文，主要功能：

- 通知子协程退出（正常退出，超时退出等）；
- 传递必要的参数。

## context.WithCancel

`context.WithCancel()` 创建可取消的 Context 对象，即可以主动通知子协程退出。返回可取消的子 Context，同时返回函数 `cancel`。

在一个或多个子协程中，通过订阅 `ctx.Done()` 管道中的消息，接收到取消信号判断是否需要退出。可以使用`select`实现。

主协程中，调用 `cancel()` 函数通知子协程退出。

```go
func reqTask(ctx context.Context, name string) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("我要死了：", name)
			return
		default:
			fmt.Println("我还没有死")
			time.Sleep(1 * time.Second)
		}
	}
}
func main() {
	ctx, cancel := context.WithCancel(context.Background())
	go reqTask(ctx, "1")
	time.Sleep(3 * time.Second)
	cancel()
	time.Sleep(3 * time.Second)
	fmt.Println("程序结束")
}
```

`context.Backgroud()` 创建根 Context，通常在 main 函数、初始化和测试代码中创建，作为顶层 Context。

## context.WithValue

如果需要往子协程中传递参数，可以使用 `context.WithValue()`。

```go
func reqTask(ctx context.Context, name string) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("我要死了：", name)
			return
		default:
			fmt.Println("我还没有死：", name)
			message := ctx.Value("value").(string)
			fmt.Println("收到信息:", message)
			time.Sleep(1 * time.Second)
		}
	}
}
func main() {
	ctx, cancel := context.WithCancel(context.Background())
	vCtx := context.WithValue(ctx, "value", "开饭啦")
	go reqTask(vCtx, "1")
	time.Sleep(3 * time.Second)
	cancel()
	time.Sleep(3 * time.Second)
	fmt.Println("程序结束")
}
```

- `context.WithValue()` 创建了一个基于 `ctx` 的子 Context，并携带了值 `value`。
- 在子协程中，使用 `ctx.Value("value")` 获取到传递的值，读取/修改该值。

Go 语言中的 [`context.Context`](https://draveness.me/golang/tree/context.Context) 的主要作用还是在多个 Goroutine 组成的树中同步取消信号以减少对资源的消耗和占用，虽然它也有传值的功能，但是这个功能我们还是很少用到。

在真正使用传值的功能时我们也应该非常谨慎，比较常见的使用场景是传递请求对应用户的认证令牌以及用于进行分布式追踪的请求 ID。

## context.WithTimeout

如果需要控制子协程的执行时间，可以使用 `context.WithTimeout` 创建具有超时通知机制的 Context 对象。

```go
func reqTask(ctx context.Context, name string) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("我要死了：", name, ctx.Err())
			return
		default:
			fmt.Println("我还没有死：", name)
			time.Sleep(1 * time.Second)
		}
	}
}
func main() {
	ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
	go reqTask(ctx, "1")
	time.Sleep(3 * time.Second)
	cancel()
	fmt.Println("主进程主动退出")
	time.Sleep(3 * time.Second)
	fmt.Println("程序结束")
}
```

- 因为超时时间设置为 2s，但是 main 函数中，3s 后才会调用 `cancel()`，因此，在调用 `cancel()` 函数前，子协程因为超时已经退出了。
- 在子协程中，可以通过 `ctx.Err()` 获取到子协程退出的错误原因。

## context.WithDeadline

`context.WithDeadline()` 则可以控制子协程的最迟退出时间。使用方法和`context.WithTimeout`类似。

```go
ctx, cancel := context.WithDeadline(context.Background(), time.Now().Add(1*time.Second))
```