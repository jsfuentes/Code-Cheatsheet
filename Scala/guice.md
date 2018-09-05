# Guice

Dependency Injection by Google for Java

## Before DI

Need to wire everything together 

```java
public class RealBillingService implements BillingService {
  public Receipt chargeOrder(PizzaOrder order, CreditCard creditCard) {
    CreditCardProcessor processor = new PaypalCreditCardProcessor();
    TransactionLog transactionLog = new DatabaseTransactionLog();
```

This relies on actual implementations of creditcardprocesser making testing difficult as well as switching implementations

### Factories?

```java
public class CreditCardProcessorFactory {
  
  private static CreditCardProcessor instance;
  
  public static void setInstance(CreditCardProcessor processor) {
    instance = processor;
  }

  public static CreditCardProcessor getInstance() {
    if (instance == null) {
      return new SquareCreditCardProcessor();
    }
    
    return instance;
  }
}
```

```java
//so
new PaypalCreditCardProcessor();
//becomes
CreditCardProcessorFactory.getInstance();
```

Now can do proper tests, but need to setup and teardown and dependencies setup as needed per inner functionfunction extractMessagesFromJade(filePath, baseDirectory, callback) {
  fs.readFile(filePath, (err, content) => {
    if (err) {
      callback(err);
    } else {
      let messages = [];
      const jadeOptions = {
        compiler: yudi,
        filename: filePath,
        basedir: baseDirectory,
        attrs: JADE_ATTRS,
        postCompile: (compiler) => {
          messages = compiler.strings;
        },
      };
      try {
        jade.compileClient(content, jadeOptions);
      } catch (e) {
        callback(e);
      }
      callback(null, {
        messages: cleanMessages(messages),
      });
    }
  });
}

## DI

Put in constructor of object 

## Guice

Map interfaces to implementations in `Module`

```java
public class BillingModule extends AbstractModule {
  @Override 
  protected void configure() {
    bind(TransactionLog.class).to(DatabaseTransactionLog.class);
    bind(CreditCardProcessor.class).to(PaypalCreditCardProcessor.class);
    bind(BillingService.class).to(RealBillingService.class);
  }
}		
```

add `@Inject` to constructor and directs Guice to use it by looking up values for each parameter