<script setup>

   import {defineProps} from "vue";


   const props = defineProps (["post" , "description" ,"image" ]);


   
</script>

<template>
     <li>
          <img :src=props.image alt="изображение">
          <h3 class="post__title">{{ props.post}}</h3>
          <p class="description__title">{{  props.description }}</p>
        </li>
</template>

<style scoped>

img {
  width: 500px; 
  height: 500px; 
  border-top-right-radius: 20px;
  border-top-left-radius: 20px;
}

li {
   background-color: rgb(226, 226, 226);
   font-family: "log";
   height: 700px;
   width: 500px;
   box-shadow: 1px;
   text-align: center;
   border-radius: 20px;
}

.post__title {
   font-family: "log";
   font-size: 25px;
   margin-bottom: 10px;
}

.description__title {
   font-family: "log";
   font-size: 15px;

}

</style>