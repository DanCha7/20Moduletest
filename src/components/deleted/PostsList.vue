<script setup>

import {onBeforeMount, ref} from 'vue';
import PostItem from "/src/components/PostItem.vue"
import Button from '/src/components/Button.vue';



const items = ref([]);

const pagination =ref(3);





async function getPosts() {
    const res = await fetch("https://de84dd1abfa0dc3c.mokky.dev/products")
    .then( (res) => res.json()
    );

    items.value = res;
}


function clearPosts() {
    items.value = [];

}

const AddNewItem = () => {
    pagination.value +=3;
};




</script>

<template>
    <div class="filterf">
        <button @click="getPosts">Смотреть посты</button>
        <button @click="clearPosts">Удалить посты</button>
    </div>
    <ul class="test">
        <PostItem v-for="item in items.slice(0 , pagination)" 
        :key="item.id"
        :post="item.post"
        :description="item.description" 
        :image="item.image"/>
        
    </ul>
     <div class="container ju">
        <Button v-if="items.length >0 " text="добавить еще" 
        :func="AddNewItem"></Button>
     </div>
</template>



<style scoped>

.filterf {
    display: flex;
    gap: 20px;
    margin-bottom: 20px;
}

.test {
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

.test {
    display: flex;
    flex-wrap: wrap;
    gap: 30px;
    
}
.is-empty{
    color: red;
    font-size: 20px;
    text-align: center;
}

</style>


<!-- // onBeforeMount(() => {
    //         (async () => {
    //             const res = await fetch(`https://de84dd1abfa0dc3c.mokky.dev/products`
    //         ).then((res) => res.json()
    //         );
        
    //         items.value = res;
        
    //         })();
    //     }); -->


<!-- // onBeforeMount(() => {
    //     (async () => {
    //         const res = await fetch(`https://de84dd1abfa0dc3c.mokky.dev/products`
    //     ).then((res) => res.json()
    //     );
    
    //     items.value = res;
    
    //     })();
    // });



    // ?page=1&Limit=3


    // const page = ref(1); -->