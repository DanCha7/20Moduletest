<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";

const isVisible = ref(false); 
let lastScrollY = 0;

const handleScroll = () => {
  if (window.scrollY > 50) { 
    isVisible.value = true; 
  } else {
    isVisible.value = false; 
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});

</script>

<template>
    <header :class="{ 'header-visible': isVisible, 'header-hidden': !isVisible }">
        <div class="header__content">
            <a class="logof" href="/">Post.ru</a>
            <nav>
                <ul>
                    <li>
                        <a href="">Список постов</a>
                    </li>
                    <li>
                        <a href="">Фото</a>
                    </li>
                    <li>
                        <a href="">Отправить(скоро будет)</a>
                    </li>
                </ul>
            </nav>
            <a href="">Войти</a>
        </div>
    </header>
</template>

<style scoped>

header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  transition: transform 0.3s ease, opacity 0.3s ease;
  background-color: white; 
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); 
  opacity: 0; 
  transform: translateY(-100%); 
}

.header-visible {
  opacity: 1; 
  transform: translateY(0); 
}

.header-hidden {
  opacity: 1; 
  transform: translateY(-100%); 
}

/* header {
    width: 100%;
    position: fixed;
} */

.logof {
    background-color: rgb(120, 249, 7);
    padding: 20px;
    border-radius: 10px;
}
.header__content {
    align-items: center;
    font-family: "log";
    display: flex;
    justify-content: space-between;
    padding: 5px 90px;
}

ul {
    display: flex;
    gap: 70px;
}



</style>


