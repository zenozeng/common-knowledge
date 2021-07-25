# Go

- Docker, Kubernetes
- Composition is central to OOP in Go

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

- 匿名函数需要递归的时候，可以先 `var iter func(i int)` 这样声明一下（Section 5.6）

### Structs

- A named struct type S can't declare a field of same type S
- If all the fields of a struct are comparable, the sturct itself is comparalbe.
- Comparable struct types may be used as the key type of a map
