<template>
  <div>
    <ul>
      <li v-for="a in photos" :key="a.id">
        <img :src="a.url" :alt="a.title">
      </li>
    </ul>
    <div class="pagi">
      <button @click="page++">More Images</button>
    </div>
  </div>
</template>


<script setup>
const page = ref(1);
const config = useRuntimeConfig();
const { data: albums, error, refresh, pending } = await useLazyAsyncData('todos', () => $fetch(config.baseUrl + '/photos'));
const photos = computed(() => {
  return albums.value.slice(0, page.value * 8);
})
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style-type: none;
  outline: 1px solid;
}


ul{
  width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

li{
  width: calc(25% - 15px);
}

li img{
  width: 100%;
}

.pagi{
  width: 1200px;
  margin: 30px auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

button{
  padding: 10px 40px;
  background: crimson;
  color: #fff;
}
</style>
 