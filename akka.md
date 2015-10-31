# Akka

[Akka 2.3.6中文文檔](http://udn.yyuap.com/doc/akka-doc-cn/2.3.6/scala/book/index.html)

[【Akka】Actor模型探索](http://jasonding1354.github.io/2015/06/26/Scala/%E3%80%90Akka%E3%80%91Actor%E6%A8%A1%E5%9E%8B%E6%8E%A2%E7%B4%A2/)

## PingPong Example 

[一個簡單的akka actor例子](http://colobu.com/2015/02/26/simple-scala-akka-actor-examples/)

``` scala
import akka.actor._

case object PingMessage
case object PongMssage
case object StartMessage
case object StopMessage

class Ping(pong: ActorRef) extends Actor {
  var count = 0
  def incrementAndPrint {count +=1; println("ping")}
  def receive = {
    case StartMessage =>
      incrementAndPrint
      pong ! PingMessage
    case PongMssage =>
      if (count > 9){
        sender ! StopMessage
        println("ping stopped")
        context.stop(self)
      } else {
        incrementAndPrint
        sender ! PingMessage
      }
  }
}

class Pong extends Actor {
  def receive = {
    case PingMessage =>
      println("pong")
      sender ! PongMssage
    case StopMessage =>
      println("pong stopped")
      context.stop(self)
      context.system.terminate()
  }
}

object  PingPong extends App {
  val system = ActorSystem("PingPongSystem")
  val pong = system.actorOf(Props[Pong], "pong")
  val ping = system.actorOf(Props(new Ping(pong)),"ping")
  ping ! StartMessage
}
```

`def incrementAndPrint {count +=1; println("ping")}`
