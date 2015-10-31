# Typesafe Docs 

Play + Scala + Akka + Spark 

[java](java.md)

[sbt](sbt.md) 

[scala](scala.md)

[akka](akka.md)

[scala/akka API](api.md)

## Reactive Maseeage Patterns with the Actor mode, applications and integration in Scala and Akka

Amdahl’s Law ，一個程式能被多核心處理器加速的程度，不會高於程式中不可平行處理的部份的倒數。

Concurrency and parallelism are different.

Concurrency describes multiple computations occurring simultaneously. 多個運算同時進行

Parallelism is concurrency but applied to achieving a single goal.

Parallelism is achieved by dividing a single complex process into smaller tasks and executing them concurrently.


----

 one actor gives no parallelism. Actors are very lightweight, so creating many actors within a single system is encouraged. Any problem can be solved by adding yet another actor.


## IntelliJ IDEA


## TypeSafe 

Typesafe provides a commercial build of Akka and related projects such as Scala or Play as part of the Reactive Platform which is made available for **Java 6** in case your project can not upgrade to Java 8 just yet. It also includes additional commercial features or libraries.

### Typesafe Activator 

Typesafe Activator gets you started with Play Framework, Akka and Scala. (**JDK6**)


## Akka

Or you can use a build tool like Maven or SBT to download dependencies from the Akka Maven repository.

[Using Akka with sbt](http://doc.akka.io/docs/akka/2.4.0/intro/getting-started.html)

`build.sbt` : 

```
name := "My Project"
 
version := "1.0"
 
scalaVersion := "2.11.7"
 
libraryDependencies +=
  "com.typesafe.akka" %% "akka-actor" % "2.4.0"
```

### Using Akka with IntelliJ IDEA

## Apache Spark

Apache Spark—Scala-based, highly performant general computation engine for large-scale data processing

