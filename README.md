<!-- # Title -->
# Marvel
  ![Demo](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/Marvel_Logo.svg/2560px-Marvel_Logo.svg.png)
  
  ---
    
  <!-- # Short Description -->

>- The user can search through all the [Marvel API](https://developer.marvel.com) and access all their specific data, such as **characters**, **comics**, **stories**, **series** and **events**. 
>- It is possible to access the data, such as **official images**, **description** and **titles** (when it is provided).
>- The application offers the possibility to add **characters** in the user's personal list to easy access. 

The application was developed to supply the requisites of a *Technical Challenge* and test myself with new technologies and processes


<!-- # Badges -->
<div style="display: inline_block"><br>
    <img height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/androidstudio/androidstudio-original.svg">
    <img height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/kotlin/kotlin-original.svg">
    <img height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg">
    <img height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg">

</div>

---

# Tags

`Android Studio` `Kotlin` `Coroutines` `MVVM` `Room` `Hilt` `Clean Architecture` `Retrofit` `OkHttp` `Paging 3` `Picasso` `Marvel API`

---

# Android Code Challenge
## Rules: 
> Description
>- 20 characters per page -> Using [Paging 3](https://developer.android.com/topic/libraries/architecture/paging/v3-overview?hl=pt-br) to supply this demand
>- Inform when the recycler view achieves it's bottom (no more data)
>- Display, when it's provided, at least 3 **stories**, **comics**, **events** and **series**
>- Use the requested [Marvel API](https://developer.marvel.com) receive data
>- Include transitions
>- Include a **search** mechanism done by name 
>- Display a favorite list -> Using [Room Database](https://developer.android.com/training/data-storage/room?hl=pt-br) to supply this demand
>- Be able to remove the favorites from the **favorite list** and from the **character details**

---


# Demo

![](https://media.discordapp.net/attachments/655489748885831713/1070094566839038033/ezgif.com-gif-maker.gif)
>- Displays the **character list** paginated by [Paging 3](https://developer.android.com/topic/libraries/architecture/paging/v3-overview?hl=pt-br), loading each page containing 20 items. 
***
![](https://media.discordapp.net/attachments/655489748885831713/1070095064178638948/ezgif.com-gif-maker-2.gif)
>- *Search* any **character** from [Marvel API](https://developer.marvel.com) with simple clicks
***
![](https://media.discordapp.net/attachments/655489748885831713/1070102220579819641/ezgif.com-gif-maker.gif)
>- Any data related to the **character** provided by [Marvel API](https://developer.marvel.com) is displayed in it's *details screen*, such as **events**, **comics**, **stories**, **series** and **description**
***
![](https://media.discordapp.net/attachments/655489748885831713/1070097122256494592/ezgif.com-gif-maker-4.gif)
>- Check any specific content with more informtation, selecting it to reach it's *details screen*
***
![](https://media.discordapp.net/attachments/655489748885831713/1070103821948305519/ezgif.com-gif-maker-4.gif)
>- *Add* and *remove* items to personalised **favorite list** from the *details screen*, *delete* and *restore* any deleted items by mistake from the *favorite screen* if necessary
***
![](https://media.discordapp.net/attachments/655489748885831713/1070099274609741885/ezgif.com-gif-maker-6.gif)
>- *Delete all* your **favorites** with few clicks if necessary
---

# Code Example
```kotlin
pclass CharacterModelPagingSource(private val api: MarvelApi):
    PagingSource<Int, CharacterModel>() {

    override fun getRefreshKey(state: PagingState<Int, CharacterModel>): Int? {
        return state.anchorPosition?.let { position ->
            val anchorPage = state.closestPageToPosition(position)
            anchorPage?.prevKey?.plus(1)?: anchorPage?.nextKey?.minus(1)
        }
    }

    override suspend fun load(params: LoadParams<Int>): LoadResult<Int, CharacterModel> {
        return try {
            val position = params.key?: STARTING_PAGE_INDEX
            val offset = position * PAGE_SIZE
            val response = api.recoverAll(offset = offset)
            val nextKey = if(offset >= response.body()?.data!!.total) {
                null
            } else {
                position + 1
            }
            return LoadResult.Page(
                data = response.body()?.data!!.results.toList(),
                prevKey = null,
                nextKey = nextKey
            )
        } catch(e: java.lang.Exception) {
            LoadResult.Error(e)
        }
    }
}
```

This is the code to supply the [Paging 3](https://developer.android.com/topic/libraries/architecture/paging/v3-overview?hl=pt-br) requisites in order to display the received content from [Marvel API](https://developer.marvel.com) in pages containing 20 items.

---

# Libraries

>- [Timber](https://github.com/JakeWharton/timber)
>- [Lifecycle](https://developer.android.com/jetpack/androidx/releases/lifecycle)
>- [Coroutines](https://developer.android.com/kotlin/coroutines?hl=pt-br)
>- [KTX](https://developer.android.com/kotlin/ktx)
>- [Navigation Components](https://developer.android.com/guide/navigation)
>- [Hilt](https://dagger.dev/hilt/)
>- [ROOM](https://developer.android.com/jetpack/androidx/releases/room?hl=pt-br)
>- [Firebase](https://firebase.google.com)
>- [Picasso](https://square.github.io/picasso/)
>- [Carousel View](https://github.com/sayyam/carouselview)
>- [Paging 3](https://developer.android.com/topic/libraries/architecture/paging/v3-overview?hl=pt-br)
>- [Retrofit](https://square.github.io/retrofit/)
>- [OkHttp](https://square.github.io/okhttp/)
>- [Marvel API](https://developer.marvel.com)
---

# Contributors

- [Thiago Rodrigues](https://www.linkedin.com/in/tods/)
