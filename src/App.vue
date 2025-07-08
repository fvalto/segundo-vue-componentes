<script setup>
  import { onMounted, ref } from 'vue';

  import BlogPost from './components/BlogPost.vue';
  import PaginateButton from './components/PaginateButton.vue';
  import LoadingSpinner from './components/LoadingSpinner.vue';

  const posts = ref([]);
  const postXpage = 5;
  const inicio = ref(0);
  const fin = ref(postXpage);
  const loading = ref(false);

  const favorito = ref('');

  const cambiarFavorito = (title) => {
    favorito.value = title;
  };

  const next = () => {
    inicio.value += postXpage;
    fin.value += postXpage;
  }

  const previous = () => {
    inicio.value -= postXpage;
    fin.value -= postXpage;
  }

  onMounted(async() => {
    loading.value = true;
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/posts')
      posts.value = await res.json()
    } catch (error) {
      console.log(error)
    } finally {
      loading.value = false;
    }
  })

  // fetch('https://jsonplaceholder.typicode.com/posts')
  //   .then((res) => res.json())
  //   .then((data) => posts.value = data)
  //   .finally(() => loading.value = false)
</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mis Posts Favoritos: {{ favorito }}</h2>
    <PaginateButton 
      @previous="previous" 
      @next="next" 
      :inicio="inicio" 
      :fin="fin" 
      :length="posts.length" 
      class="mb-2"
    />

    <BlogPost 
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title=post.title
      :id=post.id
      :body=post.body
      :colorText=post.colorText
      @elegirFavorito="cambiarFavorito"
      class="mb-2"
    />
  </div>
</template>