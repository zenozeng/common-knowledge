# Go

- Docker, Kubernetes

## 语法

```go
a[i], a[j] = a[j], a[i] // Tuple Assignment, right-hand side expressions are evaluated before any of the variables are updated
```

```go
type Weekday int

const (
  Sunday Weekday = iota
  Monday
  Tuesday
  Wednesday
  Thursday
  Friday
  Saturday
)
```

```go
type Flags uint
const (
  FlagUp Flags = 1 << iota // evaluates to successive powers of 2
  FlagBroadcast
  FlagLoopback
  FlagPointToPoint
  FlagMulticast
)
```

```go
var s []int     // len(s) == 0, s == nil
s = nil         // len(s) == 0, s == nil
s = []int(nil)  // len(s) == 0, s == nil
s = []int{}     // len(s) == 0, s != nil
```
