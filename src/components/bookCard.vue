<template>
  <div class="card" :class="borderClass">
    <img src="@/assets/points.svg" class="card__img-points" />

    <img class="card__book" :src="img" />
    <img v-if="outcome" class="card__colored" :src="getPic(pic)" />
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: "bookCard",
  props: ["img", "outcome", "pic", "borderClass"],

  setup() {
    const getPic = (pic) => {
      return require(`../assets/${pic}.svg`);
    };
    return {
      getPic,
    };
  },
};
</script>

<style lang="scss">
.m16 {
  margin: 16px;
}
.card {
  box-sizing: border-box;
  display: inline-block;
  width: 240px;
  max-height: 270px;
  padding: 20px;
  background: #ffffff;
  box-shadow: 0px 4px 4px rgba(12, 110, 214, 0.16);
  border-radius: 12px;
  position: relative;
  text-align: center;
  &__colored {
    top: 5px;
    right: 5px;
    position: absolute;
  }

  &__img-points {
    position: absolute;
    bottom: 50%;
    left: 15px;
    cursor: pointer;
  }
}
</style>
