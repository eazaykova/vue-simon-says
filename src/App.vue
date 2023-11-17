<template>
  <div id="app"><SimonSay /></div>
</template>

<script>
import SimonSay from "@/components/SimonSay.vue";
export default {
  name: "App",
  components: { SimonSay },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333;
  margin-top: 30px;
}
html {
  font-weight: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
  position: relative;
}

* {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

body {
  position: relative;
  padding: 0;
  margin: 0;
  -webkit-tap-highlight-color: transparent;
}

h1,
h2,
h3,
h4,
h5,
p,
a {
  color: inherit;
  font-size: inherit;
  font-weight: inherit;
  text-decoration: inherit;
  padding: 0;
  margin: 0;
  word-break: break-word;
  word-wrap: break-word;
}

input {
  border: none;
  background: inherit;
  font-size: inherit;
  font-family: inherit;
  color: inherit;
}

button {
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
}
input:hover,
input:active,
input:focus,
button:hover,
button:active,
button:focus {
  outline: none;
}
</style>
