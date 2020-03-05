# Coroutines

We can think of coroutines as light weight thread

## Jobs

Coroutines jobs are like subcategory of coroutines under certain scope. It is of Type `Job`.
We have `CompletableJob` which is a subclass of `Job`, but allows us to complete the job when we want without relying on coroutine to do so.

We can get a callback if the job is completed or cancelled using invokeOnCompletion

```kotlin
job.invokeOnCompletion(
            onCancelling = true,
            invokeImmediately = true,
            handler = object : CompletionHandler {
                override fun invoke(cause: Throwable?) {
                    if (job.isCancelled) {
                        Log.e(TAG, "NetworkBoundResource: Job has been cancelled...")
                        cause?.let {
                            //Job is cancelled
                        } ?:
                    } else if (job.isCompleted) {
                        //job is completed
                    }
                }
            })

```

Tutorial on this method can be found under the below link:
[Kotlin Coroutine Jobs (beginner tutorial)](https://github.com/HadySalhab/CoroutineJob-Tutorial/tree/master)

## Dispatchers

We have `Main` , `IO` & `Default` dispatchers.

To change the coroutine Dispatcher at runtime we can use `withContext(Dispatcher...)` on a coroutine.
