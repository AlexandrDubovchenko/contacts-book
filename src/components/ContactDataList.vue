<template>
  <ul>
    <li v-for="(data, i) in data" :key="i">
      <div class="data_item" v-for="(value, key) in data" :key="key">
        <span>{{ key }}: </span>
        <span v-if="!(i === editingData)"> {{ value }}</span>
        <input v-model="inputValue" type="text" v-if="i === editingData" />
        <div class="buttons">
          <button
            type="button"
            @click="
              i === editingData ? saveHandler(i, key) : editHandler(i, value)
            "
            class="btn"
          >
            {{ i === editingData ? "Save" : "Edit" }}
          </button>
          <button
            v-if="i === editingData"
            type="button"
            @click="cancelEdit"
            class="btn"
          >
            Cancel
          </button>
          <button
            type="button"
            @click="deleteHandler(i)"
            class="btn btn_delete"
          >
            Delete
          </button>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: "contact-data-list",
  props: {
    data: Array,
    saveData: Function,
    deleteData: Function,
  },
  data() {
    return {
      inputValue: "",
      editingData: null,
    };
  },
  methods: {
    saveHandler: function (index, key) {
      this.saveData(index, key, this.inputValue);
      this.editingData = null;
    },
    editHandler: function (index, value) {
      this.inputValue = value;
      this.editingData = index;
    },
    deleteHandler: function (index) {
      this.deleteData(index);
    },
    cancelEdit: function () {
      if (confirm("Are you sure")) {
        this.editingData = null;
        this.inputValue = "";
      }
    },
  },
};
</script>

<style scoped>
li {
  margin-bottom: 10px;
}
.data_item {
  font-size: 24px;
  display: flex;
  justify-content: space-between;
  padding: 10px;
  flex: 1;
}
button:not(:last-child) {
  margin-right: 5px;
}
</style>
