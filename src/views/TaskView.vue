<template>
  <div class="wrapper">
    <div class="container">
      <header class="header">
        <button @click="$router.push('/')" class="header__btn">Назад</button>
      </header>
      <button class="title-btn">В мире книг</button>

      <div class="content">
        <div class="content__left">
          <p class="invis">заглушка</p>
          <BookCard
            class="m16"
            v-for="item in items.filter((x) => x.activated == false)"
            :key="item.id"
            draggable="true"
            @dragstart="onDragStart($event, item)"
            :img="item.image"
          />
        </div>
        <div
          v-for="category in categories"
          :key="category.id"
          class="content__right"
        >
          <p class="content__paragraph" v-if="category.id === 0">
            Жанры фольклора
          </p>
          <p class="content__paragraph" v-if="category.id === 1">
            Не являются жанрами фольклора
          </p>
          <div
            class="droppable"
            v-for="i in 6"
            :key="i"
            @drop="onDrop($event, category.id)"
            @dragover.prevent
            @dragenter.prevent
          >
            <BookCard
              v-if="getItem(category, i)"
              draggable="true"
              @dragstart="onDragStart($event, getItem(category, i))"
              :outcome="outcome"
              :img="getItem(category, i).image"
              :class="{
                wrong:
                  outcome &&
                  getItem(category, i).match != getItem(category, i).categoryId,
                correct:
                  outcome &&
                  getItem(category, i).match ===
                    getItem(category, i).categoryId,
              }"
              :pic="[
                getItem(category, i).match === getItem(category, i).categoryId
                  ? 'success'
                  : 'error',
              ]"
            />
          </div>
        </div>
        <ButtonMain
          class="button-check"
          @click="checkAnswer"
          text="Проверить"
        />
      </div>
    </div>
    <FooterVue />
  </div>
</template>
<script>
/* eslint-disable */
import { ref } from "vue";
import BookCard from "@/components/bookCard.vue";
import ButtonMain from "@/components/ButtonMain.vue";
import FooterVue from "../components/FooterVue.vue";
export default {
  components: { BookCard, ButtonMain, FooterVue },
  name: "TaskView",
  setup() {
    let outcome = ref(false);

    const items = ref([
      {
        id: 0,
        categoryId: 0,
        image: require("@/assets/book1.jpg"),
        match: 1,
        activated: false,
        lain: 0,
      },
      {
        id: 1,
        categoryId: 0,
        image: require("@/assets/book2.jpg"),
        match: 1,
        activated: false,
        lain: 0,
      },
      {
        id: 2,
        categoryId: 1,
        image: require("@/assets/book3.jpg"),
        match: 0,
        activated: false,
        lain: 0,
      },
      {
        id: 3,
        categoryId: 0,
        image: require("@/assets/book4.jpg"),
        match: 1,
        activated: false,
        lain: 0,
      },
      {
        id: 4,
        categoryId: 1,
        image: require("@/assets/book5.jpg"),
        match: 0,
        activated: false,
        lain: 0,
      },
      {
        id: 5,
        categoryId: 1,
        image: require("@/assets/book6.jpg"),
        match: 0,
        activated: false,
        lain: 0,
      },
    ]);

    const categories = ref([
      {
        id: 0,
      },
      {
        id: 1,
      },
    ]);

    function getItem(category, i) {
      return items.value.find((item) => {
        return (
          item.match === category.id &&
          item.activated == true &&
          item.lain == i - 1
        );
      });
    }

    function onDragStart(e, item) {
      e.dataTransfer.dropEffect = "move";
      e.dataTransfer.effectAllowed = "move";
      e.dataTransfer.setData("itemId", item.id.toString());
      e.dataTransfer.setData("itemCatId", item.categoryId.toString());
    }

    function onDrop(e, categoryId) {
      const itemId = parseInt(e.dataTransfer.getData("itemId"));

      items.value = items.value.map((x) => {
        if (x.id === itemId) {
          x.activated = true;
          x.match = categoryId;

          let len = items.value.filter((item) => {
            return item.activated == true && item.match === categoryId;
          }).length;
          x.lain = len - 1;
        }
        return x;
      });
    }
    function checkAnswer() {
      outcome.value = true;
      window.scrollTo(0, 0);
    }
    return {
      outcome,
      items,
      categories,
      onDragStart,
      onDrop,
      checkAnswer,
      getItem,
    };
  },
};
</script>
