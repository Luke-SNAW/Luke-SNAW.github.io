
> https://javascript.plainenglish.io/closing-modals-by-pressing-the-back-button-in-vue-js-568589b4503f

On some websites, when we click somewhere like an item or picture, a modal may be opened. Eg: we have a gallery page with many pictures in a small size. When we click on a picture, a modal will be opened to show this picture in the big size. It’s a really popular and great feature. But the thing I want to mention in this article is the action to close this modal. Almost the modal gives us a way to close this modal easily like clicking to the outside or clicking on a close button like here:

As I said these ways are fine with me on the PC. But on the mobile, I see some websites give us the extra way to close the modal that I really like it. This is close a modal with a back button. In the PC, we rarely close the modal by the back button because it’s not really a friendly way. We may see that picture below, the position of the back button in the PC is so far than other places to do it:

But I think it’s not the same in the mobile view. We may take a quick look at the real example below:

We may see the position of the close button usually on the top of the phone screen. The space from our finger to the mobile back button is shorter than the close button. Besides that, as a phone user, I tend to click on the back button when I want to close something or just back to the previous thing. Following that think, I really feel not good if I open a modal and then click on the back button as a habit. And instead of closing the modal, I was brought back to the previous page. I know besides the close button, we also use this method “click to outside”. I totally agree with this option. But sometimes the modal size is so large that it takes most of the “outside” space. In this case, it may be hard to click on the outside area.

In the next parts of this article, I’ll show you some ways to handle this problem with Vue.

## Build a small demo

Before coding the solutions, I think we should build a little demo. In this demo, we have a Vue application that installed Vue-router. Let’s take a look at the coding lines we will work with today:

We have a Modal component with props `show` to control the show status of the modal. Also have a emit `onHide` to emit the hide event:

```html
<Modal :show="isShow" @on-hide="closeModal">
  <!-- content -->
</Modal>
```

We will have a parent component here:

```html
<template>
  <div>
    <Modal :show="isShow" @on-hide="closeModal">
      <div class="custom-modal">
        <img :src="imgUrl" />
      </div>
    </Modal>
    <ul>
      <li @click="openModal(image.id)" :key="image.id" v-for="image in images">
        <img :src="image.id" alt="" />
      </li>
    </ul>
  </div>
</template>
<script setup lang="ts">
  import { ref } from "vue"

  // Let assume that we have three images with this urls
  const images: { id: string; text: string }[] = [
    {
      id: "/1.jpg",
      text: "Picture 1",
    },
    {
      id: "/2.jpg",
      text: "Picture 2",
    },
    {
      id: "/3.jpg",
      text: "Picture 3",
    },
  ]

  const isShow = ref<boolean>(false)
  const imgUrl = ref<string>("")

  function closeModal() {
    isShow.value = false
  }

  function openModal(id: string) {
    imgUrl.value = id
    isShow.value = true
  }
</script>
```

In this example, we have a page containing a list of pictures. When we click on the picture, the modal which has the picture will be shown. To close it we need to click to close button on the top of the modal. If we click on the back button, we will be brought to a previous page.

I think we have an example that fits with the problem we talked about above. Let’s jump to the first solution.

## Using hash

The first solution is the simplest and most popular solution. I see many websites in both SPA and traditional applications using it. In this solution, we just need to add a hash value to the URL when opening the modal. When this modal is closed, we just need to remove this hash.

The first action is open the modal. We may keep the current action, we just need to add a step to update the hash for the URL. We may do it inside of Javascript vie Vue-router. If you don’t want to modify the script function, we may modify the template by adding the tag with the href value as the hash value you want to set.

```html
<!-- The a tag solution -->
<li @click="openModal(image.id)" :key="image.id" v-for="image in images">
  <a :href="'#' + image.id">
    <img :src="image.id" alt="" />
  </a>
</li>
```

```js
import { useRouter } from "vue-router"

const router = useRouter()

function openModal(id: string) {
  imgUrl.value = id
  isShow.value = true
  router.push({ hash: id })
}
```

Now, let's try!

It works, the hash in the URL is added when we open the modal. But when I test the mobile back button clicking. The modal is still there. But at least we won’t be brought back to the previous page. The rest of the work just handles the close modal when the hash change. As the simplest solution in this article, it’s so simple. We just need to watch the hash value with `Vue-router`. When the hash value is empty, we will close the modal. Here is the code:

```js
import { watch } from "vue"
import { useRoute } from "vue-router"

const route = useRoute()

watch(
  () => route.hash,
  () => {
    if (route.hash === "") {
      isShow.value = false
    }
  }
)
```

Let’s check it.

It’s working! But have a little thing we missed, remove the hash when the modal is closed without the back button. Let’s see what’s happen if we don’t handle this action:

We may see that after the modal is closed from the close button, the hash from the URL still existed. If the user clicks on the back button, instead of back to the previous page, it just stays on the current page and removes the hash in the URL. To handle it, just need to add one code line into the method close modal.

```js
function closeModal() {
  isShow.value = false
  router.back()
}
```

That’s the result

I think this solution works almost well. But It’s a simple solution. And It still has a critical problem. It’s hash. I know we rarely have a Vue application use a Vue router with a hash mode nowadays. But what will happen if we use this solution in a Vue application that uses hash mode? Let’s see.

It is broken! In this demo, I used the way with `<a href>`. Let’s try the way `router.push({ hash })` .

It works well, let’s jump to the next solution.

## Use the query

This is another version of the hash solution. If we can’t use the hash, we just need to use the query param instead of the hash. To do this, we just modify a bit from the above solution. Firstly, the way to use the tag may no longer be useful, I also don’t suggest this way. We will modify based on the Vue-router way inside the method function like this:

```js
import { useRouter } from "vue-router"

const router = useRouter()

function openModal(id: string) {
  imgUrl.value = id
  isShow.value = true
  router.push({
    path: route.path,
    query: {
      image_id: id,
      ...route.query,
    },
  })
}
```

Just need to replace adding hash action by pushing to the current path with a custom query param. For the detected user click to on the back button, we also watch the route change. But instead of watching the hash value, we will follow the query value. If our query “custom” param is empty, just need to close the modal. Here is the code base:

```js
watch(
  () => route.query,
  () => {
    if (!route.query.image_id) {
      isShow.value = false
    }
  }
)
```

Let’s test it:

It still works well. It seems we solved the problem from the hash solution. Let’s jump to the last solution.

## The solution without modifying the URL

This is the last solution in this article. This article has the same concept as the above solutions by flying on the wings of Vue-router. But the biggest difference is this solution doesn’t modify any part of the URL. Besides that, this solution also does not need more code to implement. If the above solutions need to modify the action open and close modal, in this solution we do not need to do this. We just need to use the hook `onBeforeRouteLeave` from Vue-router. This hook allows us to follow and control the changing of history.

```js
import { onBeforeRouteLeave } from "vue-router"

onBeforeRouteLeave((to, from, next) => {
  if (isShow.value) {
    next(false)
    isShow.value = false
  } else {
    next()
  }
})
```

If the modal is shown, we will cancel the moving of the router by `next(false)` and close the modal. Let’s check this hook.

It works! Very simple and easy to do. But this way has a little critical problem. Because we reject the first router change when the modal is shown. So it may make trouble when we want to change the router in the open modal. I’ll add a link back to the Home page. Let’s see what happens when we click on this link.

It does not work. Instead of redirecting to the Home page, It just closes the modal. Because this hook not only applies to the back button. It also applies to any redirect action. We have many ways to fix it like catching the event `popstate` of `window` with the hook `beforeEach` of Vue-router… But in this article, I just introduce you to a simple solution. This is a simple way is check the URL we will redirect to like this:

```js
import { useRouter } from 'vue-router';

const previouseUrl = useRouter().options.history.state.back;

onBeforeRouteLeave((to, \_, next) => {
 if(isShow.value) {
 if(to.fullPath === previouseUrl) {
 isShow.value = false
 next(false);
 } else {
 next();
 }
 } else {
 next();
 }
})
```

Let’s check it:

It works! I know this way isn’t really good because it can’t solve some small problems. But I think it’s a lightweight solution. This is the last solution in this article.
