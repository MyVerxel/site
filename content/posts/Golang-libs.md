---
title: "Golang-libs"
date: 1402-02-03T03:35:02
draft: false
---

### fmt

```go
fmt.Println(i)

fmt.Sprintf("%v", v)
fmt.Sprintf("%d", ip[0])

str := fmt.Sprint( int( ip[i] ) )
```

### bytes

```go
var buffer bytes.Buffer
buffer.WriteString( fmt.Sprintf("%v", v) )
return buffer.String()
```

### strconv

```go
strconv.Itoa( int(b) ) //if b str or byte
strconv.Itoa(     b  ) 
```

### strings

```go
strings.Join( arr , ".")
```

### time

```go
time.Now() // 2009-11-10 23:00:00 +0000 UTC m=+0.000000001
```