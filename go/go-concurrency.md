# Go concurrency

## Primitives
* sync.Mutex
* sync.Cond
* sync.WaitGroup
* channel

## Principles of using channel
* Owner goroutine should create, write, and close the channel.
* Consumer goroutine should only read from the channel.
* Use read-only and write-only channels to confine responsibilities to their own goroutines.

## Common patterns
* Create a channel and pass it into goroutine inside a func, and only return the read-only primitive, confining the write and close to the owner goroutine.
```go
getReadChannel = func() <-chan int {
	c := make(chan int)
	go func() {
		defer close(c)
		// do something to write to channel c
	}
	return c
}
```
* Use for-select to receive cancellation signal from parent goroutine. The channel is usually called done.
```go
go func(<-chan int readChan, <-chan int done) {
	for {
		select {
		case value <-readChan:
			// do something with received value
		case <-done:
			return
		}
	}
}
```
