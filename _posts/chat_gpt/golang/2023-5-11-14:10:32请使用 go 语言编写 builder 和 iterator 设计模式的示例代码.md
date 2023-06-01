---
layout: post
categories: golang
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
请使用 go 语言编写 builder 和 iterator 设计模式的示例代码

Answer:

你好，这是Bing。我可以用中文（简体）回答你的问题。😊

根据搜索结果，我为你找到了一些关于go语言中builder和iterator设计模式的示例代码和解释。

**builder设计模式**是一种创建型模式，用于将一个复杂对象的构建过程分离出来，使得同样的构建过程可以创建不同的表示。在go语言中，可以使用struct和方法来实现builder模式。例如，以下代码<sup>3</sup>展示了如何使用builder模式来创建一个汽车对象：

```go
package main

import "fmt"

// Car is a product object
type Car struct {
	wheel  string
	engine string
	body   string
}

// Builder is an abstract builder
type Builder interface {
	BuildWheel()
	BuildEngine()
	BuildBody()
	GetResult() *Car
}

// Director is a director
type Director struct {
	builder Builder
}

// NewDirector is a constructor for Director
func NewDirector(builder Builder) *Director {
	return &Director{builder: builder}
}

// Construct is a method for Director
func (d *Director) Construct() {
	d.builder.BuildWheel()
	d.builder.BuildEngine()
	d.builder.BuildBody()
}

// BenzBuilder is a concrete builder for Benz car
type BenzBuilder struct {
	car *Car
}

// NewBenzBuilder is a constructor for BenzBuilder
func NewBenzBuilder() *BenzBuilder {
	return &BenzBuilder{car: &Car{}}
}

// BuildWheel is a method for BenzBuilder
func (b *BenzBuilder) BuildWheel() {
	b.car.wheel = "Benz Wheel"
}

// BuildEngine is a method for BenzBuilder
func (b *BenzBuilder) BuildEngine() {
	b.car.engine = "Benz Engine"
}

// BuildBody is a method for BenzBuilder
func (b *BenzBuilder) BuildBody() {
	b.car.body = "Benz Body"
}

// GetResult is a method for BenzBuilder
func (b *BenzBuilder) GetResult() *Car {
	return b.car
}

// BmwBuilder is a concrete builder for Bmw car
type BmwBuilder struct {
	car *Car
}

// NewBmwBuilder is a constructor for BmwBuilder
func NewBmwBuilder() *BmwBuilder {
	return &BmwBuilder{car: &Car{}}
}

// BuildWheel is a method for BmwBuilder
func (b *BmwBuilder) BuildWheel() {
	b.car.wheel = "Bmw Wheel"
}

// BuildEngine is a method for BmwBuilder
func (b *BmwBuilder) BuildEngine() {
	b.car.engine = "Bmw Engine"
}

// BuildBody is a method for BmwBuilder
func (b *BmwBuilder) BuildBody() {
	b.car.body = "Bmw Body"
}

// GetResult is a method for BmwBuilder
func (b *BmwBuilder) GetResult() *Car {
	return b.car
}

func main() {
	benzBuilder := NewBenzBuilder()
	director := NewDirector(benzBuilder)
	director.Construct()
	car := benzBuilder.GetResult()
	fmt.Println(car)

	bmwBuilder := NewBmwBuilder()
	director = NewDirector(bmwBuilder)
	director.Construct()
	car = bmwBuilder.GetResult()
	fmt.Println(car)
}
```

**iterator设计模式**是一种行为型模式，用于提供一种顺序访问一个聚合对象中各个元素的方法，而又不暴露该对象的内部表示。在go语言中，可以使用for...range语法来实现iterator模式。例如，以下代码<sup>2</sup>展示了如何使用iterator模式来遍历一个通道中的元素：

```go
package main

import (
	"fmt"
)

func main() {
	ch := make(chan int)
	go func() {
		for i := 0; i < 10; i++ {
			ch <- i // write to channel ch
		}
		close(ch) // close channel ch when done writing
	}()
	for x := range ch { // read from channel ch until it's closed
		fmt.Println(x)
	}
}
```


\-
\[1]: [GitHub - senghoo/golang-design-pattern: 设计模式 Golang实现－《研磨设计模式》读书笔记](https://github.com/senghoo/golang-design-pattern)
\[2]: [Iterators - Go Language Patterns](http://www.golangpatterns.info/object-oriented/iterators)
\[3]: [Go语言设计模式实践：迭代器（Iterator） - Go语言中文网](https://studygolang.com/articles/1695)
\[4]: [GitHub - lee501/go-patterns: Golang 设计模式](https://github.com/lee501/go-patterns)

<hr/>

