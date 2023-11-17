<template>
  <div>
    <input
      type="radio"
      :value="value"
      :name="name"
      :id="forID"
      @change="onChange"
      :checked="isChecked"
    />
    <label :for="forID">{{ title }}</label>
  </div>
</template>

<script>
export default {
  name: "RadioField",
  props: {
    forID: String,
    title: String,
    value: String,
    name: String,
    isChecked: Boolean,
  },
  methods: {
    onChange() {
      this.$emit("getTime", event.target.value);
    },
  },
};
</script>
