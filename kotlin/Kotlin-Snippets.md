# Kotlin Snippets

## `with()` standard function

```kotlin
/*
* without with()
*/
  when (stateEvent) {
            is HeadlinesStateEvent.HeadlinesSearchEvent -> {
                return headlinesRepository.getTopHeadlines(
                    stateEvent.country,
                    stateEvent.category,
                    stateEvent.searchQuery,
                    stateEvent.page
                )
            }
```

```kotlin
   when (stateEvent) {
            is HeadlinesStateEvent.HeadlinesSearchEvent -> {
                return with(stateEvent,{
                    headlinesRepository.getTopHeadlines(
                        country,category,searchQuery,page
                    )
                })
            }
```

## Expression block with `when`

```kotlin
/*Without expression block*/

    override fun handleStateEvent(stateEvent: HeadlinesStateEvent): LiveData<DataState<HeadlinesViewState>> {
        when (stateEvent) {
            is HeadlinesStateEvent.HeadlinesSearchEvent -> {
                return with(stateEvent,{
                    headlinesRepository.getTopHeadlines(
                        country,category,searchQuery,page
                    )
                })
            }
            is HeadlinesStateEvent.None -> {
                return AbsentLiveData.create()
            }
        }
    }
```

```kotlin
   override fun handleStateEvent(stateEvent: HeadlinesStateEvent) = when (stateEvent) {
            is HeadlinesStateEvent.HeadlinesSearchEvent -> {
                 with(stateEvent,{
                    headlinesRepository.getTopHeadlines(
                        country,category,searchQuery,page
                    )
                })
            }
            is HeadlinesStateEvent.None -> {
               AbsentLiveData.create()
            }
        }
```

## High Order Function As Parameter

```kotlin
/*Without High Order Function*/

fun HeadlinesViewModel.setQuery(query: String) {
    val update = getCurrentViewStateOrNew()
    if (query.equals(update.headlinesFields.searchQuery)) {
        return
    }
    update.headlinesFields.searchQuery = query
    setViewState(update)
}
fun HeadlinesViewModel.setErrorScreenMsg(errorScreenMsg:String){
    val update = getCurrentViewStateOrNew()
    if (errorScreenMsg.equals(update.headlinesFields.errorScreenMsg)) {
        return
    }
    update.headlinesFields.errorScreenMsg = errorScreenMsg
    setViewState(update)
}

fun HeadlinesViewModel.setHeadlineListData(headlinesList: List<Article>) {
    val update = getCurrentViewStateOrNew()
    update.headlinesFields.headlinesList = headlinesList
    setViewState(update)
}


fun HeadlinesViewModel.setQueryExhausted(isExhausted:Boolean){
    val update = getCurrentViewStateOrNew()
    update.headlinesFields.isQueryExhausted = isExhausted
    setViewState(update)
}

fun HeadlinesViewModel.setQueryInProgress(isInProgress:Boolean){
    val update = getCurrentViewStateOrNew()
    update.headlinesFields.isQueryInProgress = isInProgress
    setViewState(update)
}

fun HeadlinesViewModel.setPage(pageNumber:Int){
    val update = getCurrentViewStateOrNew()
    update.headlinesFields.page = pageNumber
    setViewState(update)
}

fun HeadlinesViewModel.setCountry(country:String){
    val update = getCurrentViewStateOrNew()
    if (country.equals(update.headlinesFields.country)) {
        return
    }
    update.headlinesFields.country = country
    setViewState(update)
}
fun HeadlinesViewModel.setCategory(category:String){
    val update = getCurrentViewStateOrNew()
    if (category.equals(update.headlinesFields.category)) {
        return
    }
    update.headlinesFields.category = category
    setViewState(update)
}
```

```kotlin
/*high order function */
fun HeadlinesViewModel.updateViewState(operation:(HeadlinesViewState)->Unit){
    val update = getCurrentViewStateOrNew()
    operation(update)
    setViewState(update)
}
```
