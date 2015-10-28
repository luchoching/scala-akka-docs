# Sbt

http://www.scala-sbt.org/

The interactive build tool.

Use Scala to define your tasks. Then run them in parallel from the shell.

Powerful, interactive build platform for Reactive applications

sbt uses a small number of concepts to support flexible and powerful build definitions.

## build

http://www.scala-sbt.org/0.13/tutorial/Hello.html

`sbt`  then `sbt run`

build setting: `build.sbt`

[.sbt build definition](http://www.scala-sbt.org/0.13/tutorial/Basic-Def.html)

`build.properties` --> 可以指定特定sbt version

## Directory Structure

sbt uses the same directory structure as Maven for source files by default

```
src/
  main/
    resources/
       <files to include in main jar here>
    scala/
       <main Scala sources>
    java/
       <main Java sources>
  test/
    resources
       <files to include in test jar here>
    scala/
       <test Scala sources>
    java/
       <test Java sources>
```

Generated files (compiled classes, packaged jars, managed files, caches, and documentation) will be written to the `target` directory by default.

`.gitignore` 需要加入 `target`


