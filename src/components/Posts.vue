<script setup>
  import { ref } from 'vue';
  import PostItem from "/src/components/PostItem.vue";
  import Button from '/src/components/Button.vue';
  
  const items = ref([]);
  const newPost = ref({
    name: '',
    description: '',
    image: ''
  });
  const pagination = ref(3);
  
  const getPost = async () => {
    try {
      const response = await fetch('https://de84dd1abfa0dc3c.mokky.dev/products');
      const data = await response.json();
      items.value = data; 
    } catch (error) {
      console.error('Ошибка при загрузке постов:', error);
    }
  };

//   async function PostList(){
//     const res = await fetch('https://de84dd1abfa0dc3c.mokky.dev/products');
//     .then( (res) => res.json()
    
//     );
//   } -->
  
  const addNewPost = async () => {
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
        items.value.push(addedPost); 
        newPost.value = { name: '', description: '', image: ''}; 
      } else {
        console.error('Ошибка', response.statusText);
      }
    } catch (error) {
      console.error('Ошибка:', error);
    }
  };
  
  const clearPosts = () => {
    items.value = [];
  };
  
  const AddNewItem = () => {
    pagination.value += 3;
  };
  

  </script>
  <template>
    <div class="post__content">
      <h1 class="title_list">Добавить пост</h1>
      <form class="inputsit__add" @submit.prevent="addNewPost">
        <input v-model="newPost.name" placeholder="Название" required />
        <input v-model="newPost.description" placeholder="Описание" required />
        <input v-model="newPost.image" placeholder="URL" required />
        <button type="submit">Добавить пост</button>
      </form>
  
      <div class="filterf">
        <button @click="getPost">Смотреть посты</button>
        <button @click="clearPosts">Удалить посты</button>
      </div>
  
      <ul class="test">
        <PostItem v-for="item in items.slice(0, pagination)" 
                  :key="item.id"
                  :post="item.post"
                  :description="item.description" 
                  :image="item.image"/>
      </ul>
  
      <div class="container ju">
        <Button v-if="items.length > 0" text="добавить еще" 
                :func="AddNewItem"></Button>
      </div>
    </div>
  </template>
  
  <style scoped>
  .post__content {
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
  
  .inputsit__add {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
    gap: 10px;

  }
  
  .filterf {
    display: flex;
    gap: 20px;
    margin-bottom: 20px;
  }
  
  .test {
    display: flex;
    flex-wrap: wrap;
    gap: 30px;
    margin-bottom: 20px;
  }
  
  .ju {
    display: flex;
    justify-content: center;
  }
  
  Button {
    font-family: "log";
    font-size: 20px;
    color: white;
    background-color: rgb(88, 88, 88);
    padding: 10px 20px;
    border-radius: 10px;
  }
  </style>
  
  
