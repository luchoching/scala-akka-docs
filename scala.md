# Scala

檢查scala版本: 叫出scala REPL就知道了 

[Learn Scala in Y minutes](http://learnxinyminutes.com/docs/scala/)

[scala中文教學](http://www.codedata.com.tw/author/brianhsu/2)

Scala, a Java virtual machine (JVM) language, also does not implement actors as part of a programming language. 

Rather, Scala comes with an actor library–based toolkit called Akka.

Akka doesn’t attempt to implement an actor language.

Actually the Akka library/framework is a replacement for the Scala default actor library.

Besides, the scala.actors library was deprecated as of Scala 2.11,

## 範例1

``` scala 
// src/main/scala/progscala2/introscala/upper1.sc

class Upper {
  def upper(strings: String*): Seq[String] = {
    strings.map((s:String) => s.toUpperCase())
  }
}

val up = new Upper
println(up.upper("Hello", "World!"))
```

### 使用sbt + scala REPL 

``` bash
$ sbt 
> console
scala> :load ./upper1.sc 
```


### function 參數與回傳值 type宣告

``` scala 
def upper(strings: String*): Seq[String] = {
  strings.map((s:String) => s.toUpperCase())
}
```

funtion參數後面有`*` 表示 we can pass in as many comma-separated strngs as you want (including an empty list)

在function裡面, `strings`的type事實上為`WrappedArray` (就是java的array)

`Seq[String]`為有序的sequence, `Set`,`Map`為無序的, 為string sequence, 在java裡面用`Seq<...>`


`Seq[String]` where `Seq` (“sequence”) is an abstraction for collections that you can iterate through in a fixed order (as opposed to random or undefined order, like Sets and Maps , where no order is guaranteed). The actual type returned by this method will be `scala.collection.mutable.ArrayBuffer`

### function定義要用 = 的理由

scala會推斷分號以及return types,也可以忽略 argument list(如果沒有arguments的話), 避免模糊

強調fuctional programming: functions are passed as arguments to other functions, return from functions, and assigned to variables, just like with objects. 

如果 method body 只有單一expression, 可以省略大括號

### function literal

``` scala 
strings.map((s:String) => s.toUpperCase())
```

`=>` function literal就是annymous functions, 其他語言叫做`lambdas`, `closures`, `blocks` 或是 `procs`

在scala裡面, **function裡面最後一個expression就是 return value**

也有`return`, 不過少用, 只能用在method, 不能用在annoymous function

### methods vs functions 

the term `method` is used to refer to function defined within a class or object.

`Methods` have an implicit `this` reference to the object. 

`(s:String) => s.toUpperCase()`就叫`function`, 不叫method

### create instance

``` scala 
val up = new Upper
```

宣告`val`, 就像java的`final`, **read-only**

## Others


``` scala
maximumItems = if (maximumItems < 10) 10 else maximumItems
```

`Unit` 相當於 `void`:

```
def main(args: Array[String]): Unit = {
  println("Hello, world!")
}
```

scala 用`object`定義而不是`class`, object表示singleton object, 一個只有單一instance的class

`getOrElse`:

``` scala
val catalog: Catalog = 
  catalogSource.catalog(catalogSource.name) getOrElse 
DefaultCatalog()
```

scala不支援static methods, 利用companion object提供

`private var` 讓reference mutable, 但是不被object以外的member存取


scala 可用符號當function name, 例如 `!` (可以當作alias): 

``` scala
def !(message: Any):Unit {
    //...
}

actor ! SendMessage()
```

`implict`： 隱式轉換：隱式類型和顯式類型，區分的關鍵點為是否要在源碼中聲明類型：
隱式類型不需要，顯式類型需要

http://otaku.kigi.tw/2015/07/scala-other-session-10.html 


``` scala
implict val sender: ActorRef = sender()
```

`trait`(特徵) : (像java8的interface的 default method)

http://www.codedata.com.tw/java/scala-tutorial-7-trait

`case class`: create immutable Value Objects(IDDD)

http://openhome.cc/Gossip/Scala/CaseClass.html 

``` scala
case class Foo(orderId: String)

val msg = Foo("123")
```

In Scala `case classes` and `case objects` make excellent messages since they are immutable and have support for pattern matching, 
something we will take advantage of in the Actor when matching on the messages it has received. 
Another advantage `case classes` has is that they are marked as `serializable` by default.


`for`:  to, until, 

``` scala
for(conunter <- 1 to 20){
    println(counter)
}
```

iterate a collection: 

``` scala
for (ele <- Vector(1,2,3,4,5)){
    println(ele)
}
```

或是: 

``` scala
Vector(1,2,3,4,5) map {ele => println(ele)}
```

or: 

``` scala
val nums = Vector(1,2,3,4,5,6,7,8,9,10)
var evenNums = for {
    num <- nums
    if num % 2 == 0
    } yield num
```

pattern matching: 

``` scala
class Greeter extends Actor {
  var greeting = ""

  def receive = {
    case WhoToGreet(who) => greeting = s"hello, $who"
    case Greet           => sender ! Greeting(greeting)
  }
}
```

## API 

