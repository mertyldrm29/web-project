<template>


<Button />

<Influencer/>

</template>


<script setup>

import { ref } from 'vue'

import Button from '@/components/Button.vue'
import Influencer from './components/Influencer.vue';


// Menü görünürlüğü için ref kullanılıyor
const isMenuVisible = ref(false)

// Seçilen kategori durumu
const selectedCategory = ref('erkek') // Başlangıçta 'erkek' seçili

// Menü açma/kapama fonksiyonu
const toggleMenu = () => {
isMenuVisible.value = !isMenuVisible.value
}

// Kategori seçme fonksiyonu
const selectCategory = (category) => {
selectedCategory.value = category
isMenuVisible.value = true // Kategori seçildiğinde menüyü göster
}

</script>

<style scoped>
.menu-container {
position: relative;
}

.menu-button {
display: flex;
align-items: center;
border: 1px solid #fff;
background: red;
padding: 10px;
cursor: pointer;
transition: background-color 0.3s ease;
}

.menu-button:hover {
background-color: black;
}

.menu-button-text {
margin-left: 10px;
font-size: 16px;
color: white;
}

.icon-hamburger svg {
display: block;
width: 24px;
height: 24px;
stroke: white;
}

.category-selector {
display: flex;
align-items: center;
}

.category-options {
display: flex;
margin-left: 15px;
}

.category-options button {
background: none;
border: none;
color: rgb(0, 0, 0);
padding: 10px;
cursor: pointer;
}

.category-options button.active {
font-weight: bold;
color: #f39c12; /* Seçili buton için renk değişikliği */
}

.menu-list {
position: absolute;
top: 50px;
left: 0;
background-color: #000000;
color: white;
padding: 10px;
border-radius: 5px;
width: 200px;
display: none;
}

.menu-list ul {
list-style-type: none;
padding: 0;
}

.menu-list ul li {
padding: 5px;
}

.menu-list ul li a {
color: white;
text-decoration: none;
}

.menu-list ul li a:hover {
text-decoration: underline;
}

/* Menü görünür olduğunda */
.menu-list {
display: block;
}
</style>