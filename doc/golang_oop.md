title: Golang OOP
speaker: Jason Hou
<!-- transition: slide -->
theme: dark
transition: zoomin
[slide]
# Golang 面向对象
[slide]
## 面向对象特性
----
* 封装
* 继承
* 多态

[slide]

## 对象

<pre>
<code class="golang">
type rect struct {
    width int
    height int
}

func (r *rect) area() int {
    return r.width * r.height
}

func main() {
    r := rect{width: 10, height: 5}
    fmt.Println("area: ", r.area())
}
// => area: 50
</code>
</pre>

[slide]

## 继承
* Golang 使用组合替代继承 {:&.moveIn}


[slide]

## Has-a
<pre>
<code class="golang">
type Person struct {
   Name string
   Address Address
}
type Address struct {
   City   string
   Province string
}
func (p *Person) Talk() {
    fmt.Println("Hi, my name is", p.Name)
}
func (p *Person) Location() {
    fmt.Println("I’m at", p.Address.Province, p.Address.city)
}
func main() {
    p := Person{
        Name: "买买提",
        Address: Address{
            City:   "乌鲁木齐",
            Province:  "新疆",
        },
    }
    p.Talk()
    p.Location()
}
</code>
</pre>

[slide]

## Is-a

<pre>
<code class="golang">
type Citizen struct {
   Country string
   Person // 匿名字段
}

func (c *Citizen) Nationality() {
    fmt.Println(c.Name, "is a citizen of", c.Country)
}

func main() {
    c := Citizen{}
    c.Name = "阿凡提"
    c.Country = "中国"
    c.Talk()
    c.Nationality()
}
</code>
</pre> 

[slide]

## 隐式调用-语法糖

<pre>
<code class="golang">
func main() {
    c := Citizen{}
    c.Name = "阿凡提"
    c.Country = "中国"
    c.Talk()      // 这两条语句等价
    c.Person.Talk()
}
</code>
</pre> 

[slide]

## 方法重载

<pre>
<code class="golang">
func (c *Citizen) Talk() {
    fmt.Println("Hello, my name is", c.Name, "and I'm from", c.Country)
}
</code>
</pre> 

[slide]

## 多态

<pre>
<code class="golang">
func SpeakTo(p *Person) {
    p.Talk()
}
func main() {
    p := Person{Name: "阿凡提"}
    c := Citizen{Person: Person{Name: "买买提"}, Country: "中国"}

    SpeakTo(&p)
    SpeakTo(&c)
}

>  Running it will result in
>  prog.go:48: cannot use c (type *Citizen) as type *Person in function argument
>  [process exited with non-zero status]
</code>
</pre> 

[slide]

## Interface
* Golang duck-typing {:&.moveIn}
<pre>
<code class="golang">
type Human interface {
    Talk()
}
func SpeakTo(h Human) {
    h.Talk()
}
func main() {
    p := Person{Name: "阿凡提"}
    c := Citizen{Person: Person{Name: "买买提"}, Country: "中国"}

    SpeakTo(&p)
    SpeakTo(&c)
}
</code>
</pre>


[slide]

## 谢谢大家

[slide]
## One more thing
* Golang 函数式编程 {:&.moveIn}

[slide]

## 函数一等公民
<pre>
<code class="golang">
type AddFunc func(a int) int

func add1(a int) int {
  return a + 1
}
func add2(a int) int  {
  return a + 2
}

func compose(f, g AddFunc) AddFunc {

  return func (x int) int {
    return f(g(x))
  }
}

func main() {

  add3 := compose(add1, add2)

  fmt.Printf("sum =%d", add3(2))

}
</code>
</pre>

[slide]

