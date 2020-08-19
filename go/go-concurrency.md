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
		defer close(c) // owner of the channel always defer close it
		// do something to write to channel c
	}
	return c
}
```
* Use for-select to receive cancellation signal from parent goroutine. The channel is usually called done.
```go
go func(readChan <-chan int, done <-chan int) {
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
* Use 'or' channel to aggregate multiple channels. This is done recursively so we can select-case any number of channels. The aggreate channel closes whenever any one input channel closes.
```go
var or = func(channels ... <-chan interface{}) <-chan interface{}
or = func(channels ... <-chan interface{}) <-chan interface{} {
	if len(channels) == 0 {
		return nil
	}
	if len(channels) == 1 {
		return channels[0]
	}

	orDone := make(chan interface{})
	go func() {
		defer close(orDone)

		switch len(channels) {
			case 2:
				select {
					case <- channels[0]:
					case <- channels[1]:
				}
			default:
				select {
					case <- channels[0]:
					case <- channels[1]:
					case <- channels[2]:
					default <- or(append(channels[3:], orDone)...):
				}
		}
	}
}
```