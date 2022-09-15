<template>
  <div class="wraper">
    <div class="container">
      <div class="content">
        <div
          v-for="category in categories"
          :key="category.id"
          @drop="onDrop($event, category.id, category.isFolk)"
          class="droppable"
          @dragover.prevent
          @dragenter.prevent
        >
          <h4>{{ category.title }}</h4>
          <div
            v-for="item in items.filter((x) => x.categoryId === category.id)"
            :key="item.id"
            @dragstart="onDragStart($event, item)"
            class="draggable"
            draggable="true"
          >
            <!-- <h5 >{{ item.title }}</h5> -->
            <h5  :class="{'right': item.answer && outcome, 'wrong': !item.answer && outcome }">{{ item.title }}</h5>
          </div>
        </div>
      </div>
      <button @click="checkAnswer" class="btn">проверить результат</button>
    </div>
  </div>
</template>
<script>
/* eslint-disable */
import { ref } from "vue";
export default {
  name: "App",
  setup() {
    let outcome = ref(false);

    const items = ref([
      {
        id: 0,
        title: "Сказка о рыбке",
        categoryId: 0,
        isFolk: "является",
        answer: null,
      },
      {
        id: 1,
        title: "Народные песни",
        categoryId: 0,
        isFolk: "является",
        answer: null,
      },
      {
        id: 2,
        title: "Мифы древней Руси",
        categoryId: 0,
        isFolk: "является",
        answer: null,
      },
      {
        id: 3,
        title: "Автомобили мира",
        categoryId: 0,
        isFolk: "не является",
        answer: null,
      },
    ]);

    const categories = ref([
      {
        id: 0,
        title: "Произведения",
        isFolk: "не является",
      },
      {
        id: 1,
        title: "Не является фолклером",
        isFolk: "не является",
      },
      {
        id: 2,
        title: "Фольклер",
        isFolk: "является",
      },
    ]);

    function onDragStart(e, item) {
      e.dataTransfer.dropEffect = "move";
      e.dataTransfer.effectAllowed = "move";
      e.dataTransfer.setData("itemId", item.id.toString());
      e.dataTransfer.setData("isFolk", item.isFolk);
      // e.dataTransfer.setData("answer", item.answer);
    }

    function onDrop(e, categoryId, categoryisFolk) {
      const isFolk = e.dataTransfer.getData("isFolk");
      // const answer = e.dataTransfer.getData("answer");
      const itemId = parseInt(e.dataTransfer.getData("itemId"));

      // categoryisFolk === isFolk ? console.log("хорошо") : console.log("плохо");

      items.value = items.value.map((x) => {
        if (x.id == itemId) {
          x.categoryId = categoryId;
          categoryisFolk === isFolk ? (x.answer = true) : (x.answer = false);
        }
        return x;
      });
    }

    function checkAnswer() {
      outcome.value = true;
    }

    return {
      outcome,
      items,
      categories,
      onDragStart,
      onDrop,
      checkAnswer,
    };
  },
};
</script>

<style scoped>
.right {
  background-color: green;
}
.wrong {
  background-color: rgb(128, 13, 0);
}
.wraper {
  margin: 0 auto;
  max-width: 1500px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.container {
  border: 1px solid black;
  display: flex;
  justify-content: space-evenly;
  width: 100%;
  padding: 10px;
  margin: 0 auto;
  flex-direction: column;
  background-color: rgb(228, 211, 211);
}
.btn {
  max-width: 300px;
  margin: 0 auto;
  border-radius: 15px;
  background-color: coral;
  border: none;
  padding: 15px;
  cursor: pointer;
  color: aliceblue;
}
.content {
  display: flex;
  justify-content: space-between;
}
.droppable {
  padding: 15px;
  border-radius: 5px;
  background: #2c3e50;
  margin-bottom: 10px;
  width: 300px;
  height: 500px;
}
.droppable h4 {
  color: white;
}
.draggable {
  background: white;
  padding: 5px;
  border-radius: 5px;
  margin-bottom: 5px;
}
.draggable h5 {
  margin: 0;
}
</style>
