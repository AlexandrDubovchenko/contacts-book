<template>
  <form @submit="handleSubmit">
    <div class="form_inputs">
      <Input :value="title" label="Title" :inputHandler="inputTitleHandler" />
      <Input :value="value" label="Value" :inputHandler="inputValueHandler" />
    </div>
    <button type="submit" class="btn">Add</button>
  </form>
</template>

<script>
import Input from "./Input";
export default {
  name: "add-data-form",
  components: {
    Input,
  },
  props: {
    addData: Function,
  },
  data() {
    return {
      title: "",
      value: "",
    };
  },
  methods: {
    handleSubmit: function (e) {
      e.preventDefault();
      this.addData(this.title, this.value);
      this.title = "";
      this.value = "";
    },
    inputValueHandler: function (e) {
      this.value = e.target.value;
    },
    inputTitleHandler: function (e) {
      this.title = e.target.value;
    },
  },
};
</script>

<style scoped>
form {
  margin-top: 40px;
  text-align: start;
  border: 1px solid #7f7f7f;
  padding: 15px;
  border-radius: 15px;
}
.form_inputs {
  display: flex;
  justify-content: space-between;
  margin-bottom: 15px;
}
button {
  border-radius: 10px;
  background-color: #d81b60;
  color: #fff;
  font-size: 20px;
}
</style>
