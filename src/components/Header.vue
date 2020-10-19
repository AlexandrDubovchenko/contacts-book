<template>
  <header class="header">
    <h2 class="header_title">Contacts</h2>
    <div class="buttons_container">
      <button @click="addContactHandler" class="btn add_button">
        Add Contact
      </button>
      <button @click="revertHandler" class="btn">Revert</button>
    </div>
  </header>
</template>


<script>
export default {
  name: "app-header",
  methods: {
    addContactHandler: function () {
      this.$emit("toggle-add-form");
    },
    revertHandler() {
      this.$emit("revert");
    },
  },
};
</script>

<style scoped>
.header_title {
  display: inline;
  color: #fff;
}
.header {
  position: relative;
  background-color: #d81b60;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px 40px;
  position: relative;
}
button {
  background-color: #fff;
  border-radius: 6px;
  color: #d81b60;
  font-weight: 600;
}
.add_button {
  margin-right: 5px;
}
.buttons_container {
  position: absolute;
  right: 20px;
}
</style>
