<script setup>
import { ref, watch } from "vue";
import q from "../data/data.json";
import Card from "../components/Card.vue"
import gsap from "gsap"

const quizes = ref(q)
const search = ref("")

const afterEnter = () => {
    console.log("AFTER ENTER")
}
const beforeEnter = (el) => {
    // card-enter-from
    console.log("BEFORE ENTER")
    el.style.opacity = 0
    el.style.transform = "translateY(-100px)"
}
const enter = (el) => {
    // card-enter-to
    gsap.to(el, {
        y: 0,
        opacity: 1,
        duration: 0.3,
        delay: el.dataset.index * 0.3
    })
    //card-enter-active
}


watch(search, () => {
    quizes.value = q.filter(quiz => quiz.name.toLocaleLowerCase().includes(search.value.toLowerCase()))
})

</script>

<template>
    <div>

        <header>
            <h1>El Preguntón</h1>
            <input v-model.trim="search" type="text" placeholder="Búsqueda...">
        </header>

        <div class="options-container">
            <transition-group appear @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter">
                <Card v-for="(quiz, index) in quizes" :key="quiz.id" :quiz="quiz" :data-index="index" />
            </transition-group>
        </div>

    </div>
</template>

<style scoped>
.container {
    max-width: 1000px;
    margin: 0 auto;
}

header {
    margin-bottom: 10px;
    margin-top: 30px;
    display: flex;
    align-items: center;
}

header h1 {
    font-weight: bold;
    margin-right: 30px;
}

header input {
    border: none;
    background-color: rgba(128, 128, 128, 0.1);
    padding: 10px;
    border-radius: 5px;
}

.options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
}
</style>