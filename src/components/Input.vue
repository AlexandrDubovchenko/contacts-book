<template>
  <div class="form_item">
    <span> {{label}} </span>
    <input :value="value" @input="inputHandler" />
  </div>
</template>

<script>
export default {
  name: "app-input",
  props: {
    value: String,
    inputHandler: Function,
    label: String
  },
};
</script>

<style scoped>
.form_item {
  display: flex;
  flex-direction: column;
  font-size: 24px;
  margin-right: 10px;
  margin-bottom: 10px;
}
input {
  outline: 0;
  border: none;
  border-bottom: 1px solid #898080;
  font-size: 24px;
}
</style>
