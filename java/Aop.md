

# Spring AOP
- it is a model of programming
- common task across objects
- Cross cutting Concerns (Logging, Transaction, Security, Infrastructure, ... )
- Cross cutting Object: Objects that concern different than your problem domain. (Not your main business)
- 
**Old OOP approach**
- too many relationships to crosscutting objects
- a lot of boilerplate codes
- can not change in bulk, one small change end up to change a lot of places


## Aspect
the common functionality (class) that we want to use. ex, Logging
- an aspect can have multiple advices.
- **@Aspect**: convert class to a aspect
  

### Advice
the method in Aspect.
- @Before(Pointcut expression)
- @After(Pointcut expression)
- @AfterReturning(pointcut="expression",returning="nameForArgumentOnAdviceToReadReturningValue")
- @AfterThrowing(pointcut="expression",throwing="nameForArgumentOnAdviceToReadReturningException")
- @Around(Pointcut expression)> advice method must return a value
- @Pointcut(Pointcut expression)

### JoinPoint
- is a argument in a advice method that gives info about method.
- it is an optional argument

- .toString()> return pointcut expression
- .target()> return object of class that method exist within it
  
#### ProceedingJointPoint
- Argument of Around
- .proceed()> run actual target method.
- .proceed()> is throw a throwable.
### Pointcut

- Pointcut expressions
  - execution
    - **execution**(public string getName())  
    - execution(public string package.class.getName())
    - execution(public string package.\*.model.\*.getName())
    - execution(public string get*()) - Wildcard
    - execution(public * get*()) - Wildcard
    - execution(* get*()) - method should not accept argument
    - execution(* get*(*)) - method should accept argument
    - execution(* get*(..)) - No matter it has argument or not  
    - execution(* * *(..)) - For Everything
    - execution(* * org.test.javamodels.model.Circle.*(..)) - For Everything in Circle, not mather method name or parameter
    - execution(* * *(..)) - For Everything in project, , not mather method name or parameter
  - within
    - **within**(org.test.javamodels.model.Circle) - For Everything in Circle, not mather method name or parameter
    - within(org.test.javamodels.model.*) - For Everything in Model, not mather method name or parameter
    - within(org.test.javamodels.model..*) - For Everything in model and subpackages, not mather method name or parameter
  - Args
    - args(String)> all methods with a string arg
    - we can read argumen in advvice method, 
``` java
@Before("args(String))
public void aaa(String name)
{
    // we have argument here
}
  ```
- Pointcut
  - other advice can refer to this one
```java

@Before("allGetters()")
@Before("class.allGetters()") //or full addsss
@Before("allGetters() && inCircle()") //or full addsss
public void loggerAdvice()
{
    System.out.println("ding");
}
@Pointcut("execution(* getname())")
public void allGetters(){}

@Pointcut("within(org.test.javamodels.model.Circle)")
public void inCircle(){}
```


```java

@AfterReturning(Pointcut="allGetters()",returning="test")
public void loggerAdvice(Object test)
{
    System.out.println("ding"+test);
}

@Around("allGetters()")
public Object loggerAdvice(ProceedingJoinPoint p)
{
    Object returnValue = null;

    try{
        //before
        returnValue = p.proceed();
        //after returning
    }
    catch(Throwable e)
    {
        //after throwing
    }
    //finaly
    return returnValue;

}
@Pointcut("execution(* getname())")
public void allGetters(){}

```

