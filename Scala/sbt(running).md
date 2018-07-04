# sbt

Simple Build Tool 

## Creation

`set new sbt/scala-seed.g8`

## Running

```bash
sbt
run
```

`exit` quit set

## Directory

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

Build.sbt or *.sbt defines build in base dir

## Shell vs CL

command-line mode and interactive mode

- command-line mode, you run `sbt`task from your machine terminal. Once the task successfully finishes then `sbt` exits. i.e  `sbt about` 
- the interactive mode, you run - `sbt` command and it launches a `sbt` shell 

## HI



