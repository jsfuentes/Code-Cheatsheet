# Exceptions

```scala
def error(msg: String) = throw new Error(msg) 
// (msg: String) => Nothing
throw Exc

```

## Try Catch

```scala
//val result: Int = //an expression so can do this
try {
  remoteCalculatorService.add(1, 2)
} catch {
  case e: ServerIsDownException => log.error(e, "the remote calculator service is unavailable. should have kept your trusty HP.")
} finally {
  remoteCalculatorService.close()
}
```
