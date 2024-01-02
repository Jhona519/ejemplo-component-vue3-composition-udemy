<script setup>
import ButtonCounter from "./components/ButtonCounter.vue"
import BlogPost from "./components/BlogPost.vue"
import PaginatePost from "./components/PaginatePost.vue"
import { onMounted, ref } from "vue"
import LoaderSpiner from "./components/LoaderSpiner.vue";

const posts = ref([])

const postXpage = 5;
const inicio = ref(0);
const fin = ref(postXpage);

const favorito = ref("");

const cambiarFavorito = (title) => {
  favorito.value = title;
}


const next = () => {
  inicio.value = inicio.value + postXpage
  fin.value = fin.value + postXpage
}

const prev = () => {
  inicio.value = inicio.value - postXpage
  fin.value = fin.value - postXpage
}

const loading = ref(true)

onMounted(async() =>{
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts")
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally{
    setTimeout(()=>{
       loading.value=false
     },1000)
  }
})




// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then((res) => res.json())
//   .then((data) => posts.value = data)
//   .finally(() => {
//     setTimeout(()=>{
//       loading.value=false
//     },1000)
//   })
  // setimeout es opcional pero el loading.value=false es importante
</script>

<template>
  <LoaderSpiner v-if="loading"></LoaderSpiner>
  <div class="container" v-else>

    <h1>App</h1>
    <h2>Mi post Favorito: {{ favorito }}</h2>
    <!-- <ButtonCounter/> -->


    <PaginatePost @next="next" @prev="prev" class="mb-2" :inicio="inicio" :fin="fin" :maxlength="posts.length">
    </PaginatePost>

    <BlogPost v-for="post in posts.slice(inicio, fin)" key="post.id" :title="post.title" :id="post.id" :body="post.body"
      :cambiarFavorito="cambiarFavorito" class="mb-3"></BlogPost>
  </div>
</template>

<style></style>