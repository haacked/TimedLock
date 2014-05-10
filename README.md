TimedLock
=========

A Lock structure with timeout and stack traces in case of deadlock

Here's the original blog post that introduces the concept from Ian Griffiths.

* [http://www.interact-sw.co.uk/iangblog/2004/03/23/locking](http://www.interact-sw.co.uk/iangblog/2004/03/23/locking)

I wrote a series of blog posts trying to improve on this.

* [A lock statement with timeout](http://haacked.com/archive/2004/03/26/lock-statement-with-timeout.aspx/)
* [A TimedLock success story](http://haacked.com/archive/2004/08/06/timedlock-success-story.aspx/)
* [TimedLock Revisited](http://haacked.com/archive/2004/04/17/timedlock-revisited.aspx/)
* [TimedLock Yet Again Revisited...](http://haacked.com/archive/2004/05/12/timedlock_yet_again_revisited.aspx/)
* [TimedLock with stack traces strikes back](http://haacked.com/archive/2004/10/13/TimedLockWithStackTracesStrikesBack.aspx/)

I finally moved the code into this Repository.

## Usage Exampls

```csharp
try
{
    TimedLock timeLock = TimedLock.Lock(obj);
    //Thread safe operations
    timeLock.Dispose();
}
catch(LockTimeoutException e)
{
    Console.WriteLine("Couldn't get a lock!");
    StackTrace otherStack = e.GetBlockingThreadStackTrace(5000);
    if(otherStack == null)
    {
        Console.WriteLine("Couldn't get other stack!");
    }
    else
    {
        Console.WriteLine("Stack trace of thread that owns lock!");
    }
}
```

Note, you'll only ever get the other stack trace in `DEBUG` builds.
