<template>
  <router-view />
</template>
<style lang="scss">
html {
  box-sizing: border-box;
}

*,
*::after,
*::before {
  box-sizing: inherit;
}

ul[class],
ol[class] {
  padding: 0;
}

ul[class] {
  list-style: none;
}

input,
button,
textarea,
select {
  font: inherit;
}

a {
  text-decoration: none;
}

body {
  margin: 0;
  background-color: #ecf6e9;
  font-family: "Inter";
}
#app {
  font-family: "Inter";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #ecf6e9;
}
</style>
