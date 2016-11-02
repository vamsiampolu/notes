**Communication Sequential Processes**

This is based on [talk by Eric Shull](https://www.youtube.com/watch?v=3gXWA6WEvOM) and [talk by Stuart Holloway](https://www.youtube.com/watch?v=VrmfuuHW_6w)

Implemented in the Go programming language. Clojure has a core.async library, Python and Ruby use the language mechanisms to implement this pattern.

When using multiple threads, one finds that sharing memory can lead to non-deterministic outputs. It can also be leaky because it might have to interact with multiple threads and are non composable

Erlang and Scala have the `actor` model to handle concurrency.

Unix has a simple parallel mechanism called `pipes`.

CSP is a mechanism described by C.A.R Hoare in 1978, it is known as pi calculus. It is conceptually sound and based on mathemetical rigor.

CSP is built on 2 primitives:

1. Processes

> an ordered sequence of operations, no shared memory, if one process has some data, no other process has access to it.

2. Channels

> a mechanism by which processes communicate, you can pass a channel to another channel. once you pass a value, you lose access to it.

One - to - One (pub/sub)
One - to - Many (depends on who takes the value first)
Many - to - One
Many - to - Many

CSP is synchronous, when a value is put onto a channel, the process waits until something else picks it up. In theory, only one value can be placed onto a channel. In practice, the channel can buffered to take multiple values.

> you can sync between different processes

Processes do not have knowledge of each other, they can only interact with one another based on channels. In the actor model, you have an understanding that you are passing data to another instance of an actor.

Rob Pike Squeak -> NewSqueak -> Go

Process is called a GoRoutine in Go, CSP channels are one way channels but in practice, two-way channels are used. A GoRoutine is not a thread, it is a function, it is really lightweight.

An example is to do async i/o using goroutines. Here we make a call to a server within a `goroutine`, once we recieve a value from the goroutine, we push it to a channel. 

```
func main() {
	//create a channel
	done := make(chan bool)
	result := ""
	go func() {
		resp, _ := http.Get(url)
		b,_ := ioutil.ReadAll(resp.Body)
		print(string(b))
		//push value to a channel
		done <- true
	}

	go func() {
		resp, _ := http.Get(url)
		b,_ := ioutil.ReadAll(resp.Body)
		print(string(b))
		//push value to a channel
		done <- true	
	}

	go func() {
		resp, _ := http.Get(url)
		b,_ := ioutil.ReadAll(resp.Body)
		print(string(b))
		done <- true
	}

	//wait for a value to be pushed onto the goroutine and return the value
	result += <-done
	result += <-done
	result += <-done	
}
```

If you had blocked after each call, it would be synchronous because the channel waits for a value to be pushed.

Parallelism vs concurrency
parallelism is multiple things happening at once(needs multiple processes), concurrency is dealing with a lot at once(can do one core). concurrency is still doing one thing at once.

CSP can be used for event-coordination between processes. It can also be used for sharing, one of `Go`'s mottos is that:

```
Dont communicate by sharing memory, share memory by communicating
```

---

Objects and function chains makes terrible machines. direct connection between two objects is a problem.
callback hell. A solution would be queues with real threads. Threads are expensive.

`core.async` is a first class conveyance that is like queues. The machine that acts on input from queues is known as a `process`. A process is a small scope of control. Can be used in the JVM and the browser.

Communication Sequential Processes:

1.Processes

2. Channels

When something is placed on a channel, block until it can be picked up by something else. You can build a system composed of lots of tiny sequential things.

multi read/write: In Unix, it is called `select`

Channels can have `buffers`.

Two first class process abstractions:

1. `thread`

> available in systems that have real threads

2. `go`

> available in systems where threads are not available, creates magic callback hell in the background for the browser.

There are two operations:

go:

1. Put: >!
2. Take: <!

threads:

1. Put: >!!
2. Take: <!!

To integrate with external things:

1. Put: put!
2. Take: take!

Here, we might take an event from a browser and put it on a channel. 

Symbol types are used to name programmatic constructs, keywords evaluate to themselves.

Lists are evaluated differently in clojure, the first item in a list is treated as a function. The rule for symbol is to look up the data associated with this.

(defn 
	greet
	docstr
	[args]
	(body)	
)

This is how we define a named function in clojure. A `go` routine can be stuck, we dont care about that. Write your program as a series of infinite loops and just let them do their thing.

Multiplexing and demultiplexing

connect channels using:

pipe join two channels together
merge join two channels into a new channel
split split a channel into multiple channels
mult dynamically create a channel that other channels can tap into
tap allows processes to tap into other channels
mix allows multiple processes to interact with a single channel
pub publish information based on topics
sub 

A process can talk to a single channel at a time. `alt` lets you wait on multiple operations at once. It races these channels and sees which one gives a value first.

`core.async` is an implementation of `CSP`. In `clojure`,`alt` supports priority.

The examples are in [this repo](https://github.com/cognitect/async-webinar)

Dependency Injection is an orchestration technology

Channels can block immediately, channels can have a buffer and block when full, channels can also have buffers that drop the oldest or the newest values when the buffer is full.

Paul Butcher Seven concurrency models in seven weeks. Actor model uses mailboxes...
Queues and Processes are more primitive than channels.

Actor model means that we have a unified model for in process and out of process stuff.

om is a library that uses `Clojurescript` and `React`.

There is a library that does it for Java using `jcsp`.

Can we use communicating sequential processes within koa?

Think smaller. Build your program one line at a time.