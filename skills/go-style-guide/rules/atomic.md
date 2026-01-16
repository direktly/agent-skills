# Use sync/atomic typed atomics (Go 1.19+)

Atomic operations with the [`sync/atomic`] package originally operated on raw
numeric types (`int32`, `int64`, etc.) via functions like `atomic.AddInt64`,
which made it easy to accidentally read or write the underlying variable
without using an atomic operation.

Starting with Go 1.19, the standard library introduced *typed atomic values*
such as `atomic.Bool`, `atomic.Int64`, and `atomic.Pointer[T]`. These provide
type safety and a cleaner, method-based API similar to what third-party
libraries like `go.uber.org/atomic` previously offered.

Prefer the standard library over external wrappers whenever possible. This
reduces dependencies, minimizes supply-chain risk, and keeps concurrency
primitives fully aligned with the Go toolchain.

> Note: For Go versions prior to 1.19, typed atomics do not exist in the
> standard library. In such cases, using a wrapper library (like
> `go.uber.org/atomic`) can still be considered to improve safety and
> readability.

[sync/atomic]: https://pkg.go.dev/sync/atomic

<table>
<thead><tr><th>Bad</th><th>Good</th></tr></thead>
<tbody>
<tr><td>

```go
type foo struct {
  running int32  // atomic
}

func (f *foo) start() {
  if atomic.SwapInt32(&f.running, 1) == 1 {
    // already running…
    return
  }
  // start the Foo
}

func (f *foo) isRunning() bool {
  return f.running == 1  // race!
}
```

</td> <td>

```go
type foo struct {
  running atomic.Bool
}

func (f *foo) start() {
  if f.running.Swap(true) {
    // already running…
    return
  }
  // start the Foo
}

func (f *foo) isRunning() bool {
  return f.running.Load()
}
```
</td></tr>
</tbody></table>
