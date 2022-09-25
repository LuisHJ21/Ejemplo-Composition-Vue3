<script setup>
  import BlogPost from './components/BlogPost.vue';
  import {ref,computed, onMounted} from 'vue'
  import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue'; 


  const posts = ref([])
  const favorito =ref('')
  const postxpag=10
  const inicio=ref(0)
  const fin=ref(postxpag)

  const loading=ref(true)

  const cambiarFavorito= (title)=>
  {
    favorito.value=title;
  }

  const next=()=>
  {
    inicio.value=inicio.value + postxpag
    fin.value=fin.value+postxpag
  }

  const prev=()=>
  {
    inicio.value=inicio.value - postxpag
    fin.value=fin.value-postxpag
  }

  /* onMounted(async()=>
  {
    //loading.value=true

    try {
      const res=await fetch('https://jsonplaceholder.typicode.com/posts')
      posts.value= await res.json()
      
    } catch (error) {
        console.log(error)
    }
    finally
    {
      setTimeout(() => {
      loading.value=false
    }, 2000);
    } 
  })*/

  const maxLength=computed(()=>posts.value.length)

  const fetchData=async ()=>
  {
    try {
      const res=await fetch('https://jsonplaceholder.typicode.com/posts')
      posts.value= await res.json()
      
    } catch (error) {
        console.log(error)
    }
    finally
    {
      setTimeout(() => {
      loading.value=false
    }, 2000);
    } 
  }

  /* fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res=>res.json())
  .then(data=>posts.value=data)
  .catch((e)=>console.log(e))
  .finally(()=> {
    setTimeout(() => {
      loading.value=false
    }, 2000);
  })
 */

 fetchData()
</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mis Post Favoritos: {{favorito}}</h2>
    

    <PaginatePost @prev="prev" @next="next" :inicio="inicio" :fin="fin" :limit="maxLength" class="mb-2"></PaginatePost>

    <BlogPost class="mb-2"
    v-for="post in posts.slice(inicio,fin)" :key="post.id"
    :title="post.title"
    :body="post.body"
    :id="post.id"
    @cambiarFavoritoNombre="cambiarFavorito"
    />
    
    
  </div>
  
</template>