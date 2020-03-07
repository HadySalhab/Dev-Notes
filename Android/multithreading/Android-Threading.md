# Multithreading in Android

In Android, every Application has its own stand alone `task` and stand alone `sandbox` which together constitute a `process`.

One Application can't access the environment of another application (security)

In Android, each process can host one or more tasks. These are threads.
Threads share the execution environment (`sandbox`) of the parent process, so they can communicate and exchange data easily.

Whenever we start a new thread, OS run the threads preemptively (OS has its own algorithm, to jump from one thread into another)

**Multithreading:** Decomposition of application's logic into multiple concurrent tasks.

## Thread

Two way to instantiate a thread

> FIRST-METHOD:

```java
public class MyThread extends Thread{
  private final int mSeed;

  public MyThread(int seed){
    mSeed = seed;
  }
  @Override
  public void run(){
    //
  }
}

//Inheritance
Thread thread = new MyThread(int);
thread.start(); //to fire the run method
```

> SECOND-METHOD: (`PREFERABLE`)

```java
//Preferable way
Runnable runnable = new Runnable(){
  @Override
  public void run(){
    //....
  }
}

//Composition
Thread thread = new Thread(runnable);
thread.start(); //to fire the runnable
```

## Garbage Collector

System process which automattically reclaims memory by discarding objects that are no longer in use.

> An object is considered eligible to Garbage Collection, when its **NOT** REACHABLE, which means, it has no reference to it.

### Object Reachability

![](reachability.jpg);

_Example_

![](reachability-example.jpg);

_special-case_

![](circular-ref.jpg);
