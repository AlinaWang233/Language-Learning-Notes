# Go
## Basic Grammar
Structure:
```Go
package

import

func funcName(){

}
```
Build/Run a program:

`go run pathToFile` : compile+run

`go build pathToFile`: compile to a exe.

Type:
`int, boolean, float, string`

Declaration:
```Go
var a = something
var a int = some integer
a := something
```

Loop:

only `for` no `while`
```Go
for {
    //infinite loop
}
for i:= 0; i < 9; i++{

}
break, continue
```

Switch
no need to break to jump out of switch = if else
```Go
switch a {
    case 1:
    case 2:
    case 3, 4:
    default:
}

switch{
    case t < 12:
    default:
}
```

Array:
```Go
//declare
b := [3]int{1,2,3}
var a[5]int
var twoD[2][3]int
//assign
a[4] = 100
len := len(a)
for i:=0; i< 2; i++{
    for j:=0; j <3; j++{
        twoD[i][j] = i+j
    }
}
```
make 切片/map
```Go
s :=make([]string,3)
s[0] = "a"
s[1] = "b"
s[2] = "c"

s = append(s, "d")//扩容+copy
s = append(s, "e", "f")

c:= make([]string, len(s))
copy(c,s) //[a b c d e f]

s[2:5]// [c d e]
s[:5]// [a b c d e]
s[2:]// [c d e f]


m := make(map[String]int)
m["one"] = 1
m["two"] = 2

r, ok := m["unknow"] // 0 false(does not contain key)

delete(m,"one")

for i, num := range nums{
    //index val
}

for k, v:= range m{
    //key value
}

```

function
```Go
func add(a int, b int) int{
    return a + b;
}

func add2(n int){
    n += 2 //won't change the value of n
}

func add2ptr(n *int){
    *n += 2//will change the value of n
}

func main(){
    n := 5
    add2(n)// 5
    add2ptr(&n)//7
}
```

Struct
```Go
type user struct{
    name string
    password string
}

func (u user) checkPassword(password string) bool{
    return u.password == password
}

func main(){
    a := user{name:"wang", password:"1024"}
    a.checkPassWord("2048")//false
}
```

Error handling: (type error)
```Go
func fundUser(users []user, name string) (v *users, err error){
    for _, u := range users{
        if u.name == name{
            return &u, nil
        }
    }
    return nil, errors.New("not found")
}
```

String
Methods:
```Go
Contains, Count, HasPrefix, HasSuffix, Index, Join, Repeat(string, times), Replace, Split,ToLower, ToUpper
```
Output:
```Go
fmt.Printf("s=%v\n", s)
fmt.Printf("s=%+v\n", s)//more info
fmt.Printf("s=%#v\n", s)//even more info

fmt.Printf("s=%.2f\n", f)// float with 2 digits
```

JSON
`import "encoding/json"`
```Go
a := userInfo // a struct
buf, err := json.Marshal(a) // convert to JSON & error handling

var b userInfo
err = json.Unmarshal(buf, &b)//convert buf to b and output whether there's an error
```

Time
`import "time"`
```GO
    now:= time.Now()
    t.Year(), t.Month(), t.Day()
    time.Date()
    time.Sub(); 
```

Conversion
`import "strconv"`
```GO
    strconv.ParseFloat("1.234", 64)
    strconv.ParseInt("111". 10, 64)
    strconv.ParseInt("0x1000", 0,64)
    strconv.Atoi("123")
```


## Concurrent Programming in Go
Go Routine:
`go func` would initiate a routine

CSP(Communicating Sequential Processes):
Share storage with communication instead of realizing communication by sharing storage
通过通信来实现共享内存

Channel
```Go
make(chan int) //无缓冲
make(chan int, 2) //有缓冲
//元素类型 缓冲大小
```
Sync

lock

waitgroup
- add() // add the count of a routine
- done() // decrease the count
- wait() // pause until the count is 0

## Dependencies
GOPATH: version control of packages(when package upgraded, a func might not existed anymore)
Go Vendor: imcompatibility of different versions of packages
Go Module: solved the problems of above

三要素
- go.mod 配置文件，描述依赖
[Module Path] [Version/Psudo-version]
Version: Major.Minor.Patch
Psudo-version: (based on commit) version-time-hashcode

A-> B -> C 
direct （A B）vs. indirect （A C）

incompatible
选择满足本次构建的最低版本 (1.3, 1.4 compatible & 1.3 might contain methods not in 1.4, so choose 1.4)

- Proxy 中心仓库管理依赖库 : distribute dependencies
Github SVN ... to developer: not stable, reliability of dependencies, and more pressure on code hosting platform(github)

- go get/mod 本地工具
```cmd
go get example.org/pkg @something
@update
@none delete dependencies
@version
@commit-version
@master: latest commit of the branch
```

go mod
```cmd
go mod init
go mod download
go mod tidy //添加需要的 删除不需的
```

## Test
Format: _test.go
```Go
func TestXxx(*testing.T)
func TestMain(m *testing.M){
    code := m.Run()
}

import "github.com/stretchr/testify/assert"
assert.Equal(t, expectOutput, output)
```

Unit Test单元测试 - Dependency
Unit - File/DataBase/Cache => 幂等， 稳定 - Mock

Mock
monkey: (does not depend on local test file?)
`Patch(target, replacement interface)`
`Unpatch(target interface）`

基准测试
```Go
BenchMarkSelect(b *testing.B)
BenchMarkFastSelect() int{
    return ServerIndex[fastrand.Intn(10)]// instead of rand
}
```

           Model(Data CRUD)    Entity(logic)   View(inteface/API)
File    -> Repository       -> Service      -> Controller   -> Client

Benchmark

Slice预分配内存 用copy代替reslice（释放大内存）

map预分配内存

Speed：strings.Builder (byte array)>ByteBuffer (byte array byte2string alloc space) > plus(string immutable -> alloc new space)
预分配内存：builder.grow

empty struct to save space used as placer（有占位语义不占内存）ex. empty struct to implement set (used only key not value)

mutex lock - Operating System - worse efficiency
atomic - hardware - better efficiency
## pprof
`go tool pprof -http:8080 "http://localhost:6060/debug/[command]`
top: time of function
flat: itself;
cum: itself + function called;

list: time of line

web: visualization of relation

heap: allocated space
alloc_objects; inuse_objects;
alloc_space; inuse_space;

goroutine - 协程





