
<script setup>
import { defineProps } from "vue"
import { useRouter } from "vue-router"

const router = useRouter()
const { quiz } = defineProps(['quiz'])

const navigateToQuiz = () => {
    router.push(`/quiz/${quiz.id}`)
}


</script>

<template>
    <div class="card" @click="navigateToQuiz">
        <img :src="quiz.img" alt="">
        <div class="card-text">
            <h2>{{ quiz.name }}</h2>
            <p> {{ quiz.questions.length }} Preguntas</p>
        </div>
    </div>
</template>

<style>
/*Card*/

.card {
    flex-basis: calc(33.33% - 20px);
    box-sizing: border-box;
    overflow: hidden;
    border-radius: 2%;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 35px;
    margin-right: 20px;
    cursor: pointer;

}

.card img {
    width: 100%;
    height: 190px;
    margin: 0
}

.card .card-text {
    padding: 0.5px;
    margin-left: 10px;
    margin-bottom: 5px;
    text-align: center;
    background-color: rgb(255, 255, 255);
}

.card .card-text h2 {
    font-weight: bold;
}
</style>