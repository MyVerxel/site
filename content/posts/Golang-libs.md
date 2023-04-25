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

fmt.Fprintf(conn, text)
```

#### Printf

[فایل pdf](https://raw.githubusercontent.com/saturn99/learngo/master/07-printf/printf%20cheatsheet.pdf)

![Printf Format](/image/allpPintfFormat.jpg)

```go
  var (
    planet   = "venus"
    distance = 261
    orbital  = 224.701
    hasLife  = false
  )

  // swiss army knife %v verb
  fmt.Printf("Planet: %v\n", planet)
  fmt.Printf("Distance: %v millions kms\n", distance)
  fmt.Printf("Orbital Period: %v days\n", orbital)
  fmt.Printf("Does %v have life? %v\n", planet, hasLife)

  fmt.Printf("Orbital Period: %f days\n", orbital)
  fmt.Printf("Orbital Period: %.0f days\n", orbital)
  fmt.Printf("Orbital Period: %.1f days\n", orbital)
  fmt.Printf("Orbital Period: %.2f days\n", orbital)

  // Planet: venus
  // Distance: 261 millions kms
  // Orbital Period: 224.701 days
  // Does venus have life? false
  
  // Orbital Period: 224.701000 days
  // Orbital Period: 225 days
  // Orbital Period: 224.7 days
  // Orbital Period: 224.70 days
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
strconv.Itoa(rr.t) // convert int to strint
```

### strings

```go
strings.Join( arr , ".")
```

### time

```go
time.Now() // 2009-11-10 23:00:00 +0000 UTC m=+0.000000001
```