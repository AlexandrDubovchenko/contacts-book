<template>
  <form class="form">
    <div class="controls">
      <button type="submit" @click="saveContact" class="btn btn_controls btn_save">
        Save Contact
      </button>
      <button type="button" @click="handleCancel" class="btn btn_controls">Cancel</button>
    </div>
    <Input
      label="Name"
      :value="newContactName"
      :inputHandler="inputNameHandler"
    />
    <Input
      label="Avatar URL"
      :value="newContactAvatarUrl"
      :inputHandler="inputAvatarHandler"
    />
    <div>
      <span>Contact information:</span>
    </div>
    <div class="data_container">
      <ContactDataList
        :data="newContactData"
        :deleteData="deleteData"
        :saveData="saveData"
      />
    </div>
    <AddDataForm :addData="addContactData" />
  </form>
</template>

<script>
import AddDataForm from "./AddDataForm";
import Input from "./Input";
import ContactDataList from "./ContactDataList";

export default {
  name: "add-contact-form",
  components: {
    AddDataForm,
    Input,
    ContactDataList,
  },
  data() {
    return {
      newContactName: "",
      newContactAvatarUrl: "",
      newContactData: [],
    };
  },
  methods: {
    inputNameHandler: function (e) {
      this.newContactName = e.target.value;
    },
    inputAvatarHandler: function (e) {
      this.newContactAvatarUrl = e.target.value;
    },
    addContactData: function (title, value) {
      this.newContactData.push({ [title]: value });
    },
    deleteData: function (index) {
      this.newContactData = this.newContactData.filter((d, i) => i !== index);
    },
    saveData: function (index, key, inputValue) {
      this.$set(this.newContactData, index, { [key]: inputValue });
    },
    saveContact: function (e) {
      e.preventDefault()
      this.$emit("add-contact", {
        id: this.newContactName.trim().toLowerCase().split(" ").join("_") + Math.random(),
        name: this.newContactName,
        avatar: this.newContactAvatarUrl,
        data: this.newContactData,
      });
    },
    handleCancel: function() {
      this.$emit("toggle-add-form")
    }
  },
};
</script>

<style scoped>
.form {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 700px;
  text-align: start;
  background: #fff;
  padding: 15px;
  border-radius: 15px;
  font-size: 24px;
}
.btn_controls {
  border-radius: 10px;
}
.btn_save {
  background-color: #3fbc3a;
  margin-right: 5px;
  color: #fff;
}
.controls {
  text-align: end;
}
</style>
