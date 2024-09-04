<script setup>

import { ref } from 'vue';

const posts = ref([]);
const newPost = ref({
  name: '',
  description: '',
  image: ''
});

const fetchPosts = async () => {
  try {
    const response = await fetch('https://de84dd1abfa0dc3c.mokky.dev/products');
    const data = await response.json();
    posts.value = data; 
  } catch (error) {
    console.error('Ошибка при загрузке постов:', error);
  }
};

const addPost = async () => {
  try {
    const response = await fetch('https://de84dd1abfa0dc3c.mokky.dev/products', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(newPost.value)
    });

    if (response.ok) {
      const addedPost = await response.json();
      posts.value.push(addedPost); 
      newPost.value = { name: '', description: '', image: '' }; 
    } else {
      console.error('Ошибка', response.statusText);
    }
  } catch (error) {
    console.error('Ошибка:', error);
  }
};

fetchPosts();
</script>
<template>
    <div class="list__add">
    <h1 class="title_list">Добавить свой пост</h1>
         <form class="inputsit__add" @submit.prevent="addPost">
            <input v-model="newPost.name" placeholder="Название поста" required />
             <input v-model="newPost.description" placeholder="Описание поста" required />
            <input v-model="newPost.image" placeholder="URL изображения" required />
            <button type="submit">Добавить пост</button>
      </form>
  </div>
</template>
<style scoped>
.list__add {
  text-align: center;
  font-size: 40px;
    padding: 50px 0px;
    font-family: "log";
}
input {
    width: 100%;
    border-radius: 10px;
    font-size: 20px;
}
.inputsit__add{
    display: flex;
    flex-direction: column;
    gap: 10px;

}
</style>