<template>
  <button class="button" v-bind:type="type" @click="onClick">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    type: {
      type: String,
      default: function () {
        return "button";
      },
    },
  },
  methods: {
    onClick() {
      this.$emit("game");
    },
  },
};
</script>

<style scoped>
.button {
  padding: 0 16px;
  width: 100px;
  border-radius: 4px;
  line-height: 30px;
  color: #fff;
  background-color: #5181b8;
  cursor: pointer;
}

.button:hover {
  opacity: 0.88;
}
</style>
