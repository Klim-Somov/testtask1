<template>
  <div class="wrapper">
    <div class="container container__home">
      <h1 class="container__heading">В мире книг</h1>
      <div class="instruction">
        <h2 class="instruction__heading">Инструкция:</h2>
        <div class="instruction__des">
          Распредели книги, ориентируясь на названия, по соответствующим
          рубрикам таблицы: «Жанры фольклора», «Не являются жанрами фольклора
        </div>
      </div>
      <ButtonMain @click="$router.push('task')" text="Продолжить" />
    </div>
  </div>
</template>
<script>
/* eslint-disable */
import ButtonMain from "@/components/ButtonMain.vue";
export default {
  name: "HomeView",
  components: {
    ButtonMain,
  },
};
</script>
