<script setup>
import { defineProps  } from 'vue';

const props = defineProps(["text" , "func" ]);
</script>

<template>
    <button @click="func">{{ props.text }}</button>




</template>

