<template>
  <div class="contact">
    <div class="controls">
      <button @click="isEditing ? changeContact() : setIsEditing()" class="btn">
        {{ !isEditing ? "Edit" : "Save" }}
      </button>
      <button @click="deleteContact(contact.id)" class="btn btn_delete">Delete</button>
    </div>
    <div class="title">
      <h2 v-if="!isEditing">{{ contact.name }}</h2>
      <input type="text" v-model="name" v-if="isEditing" />
    </div>
    <img width="500" height="500" :src="contact.avatar" alt="ava" />
    <div v-if="isEditing">
      <label for="input_avatar">AvatarUrl:</label>
      <input id="input_avatar" type="text" v-model="avatar" />
    </div>
    <ContactDataList
      :data="contact.data"
      :deleteData="deleteData"
      :saveData="saveData"
    />
    <AddDataForm v-bind:addData="addData" v-if="isEditing" />
  </div>
</template>


<script>
import AddDataForm from "../components/AddDataForm";
import ContactDataList from "../components/ContactDataList";
export default {
  name: "Contact",
  props: {
    contacts: Array,
  },
  components: {
    AddDataForm,
    ContactDataList,
  },
  data() {
    return {
      isEditing: false,
      name: "",
      avatar: "",
    };
  },
  computed: {
    contact() {
      return this.contacts.filter(
        (contact) => contact.id === this.$route.params.id
      )[0];
    },
  },
  methods: {
    addData: function (title, value) {
      this.$emit("add-data", {
        id: this.contact.id,
        title,
        value,
      });
      this.newKey = "";
      this.newValue = "";
    },
    deleteData: function (index) {
      if (confirm("Are you sure")) {
        this.$emit("delete-data", {
          id: this.contact.id,
          index,
        });
      }
    },
    saveData: function (index, key, inputValue) {
      this.$emit("change-data", {
        id: this.contact.id,
        index,
        value: { [key]: inputValue },
      });
      this.editingData = null;
    },

    changeContact: function () {
      this.$emit("change-contact", {
        id: this.contact.id,
        name: this.name,
        avatar: this.avatar,
      });
      this.isEditing = false;
    },
    setIsEditing: function () {
      this.name = this.contact.name;
      this.avatar = this.contact.avatar;
      this.isEditing = true;
    },
    deleteContact: function (id) {
      if (confirm("Are you sure?")) {
        this.$emit("delete-contact", id);
        this.$router.push({name: 'Home'})
      }
    },
  },
};
</script>

<style scoped>
.title {
  margin-bottom: 10px;
}

.controls {
  text-align: end;
}
.controls button {
  margin-right: 10px;
}
label {
  font-size: 24px;
  margin-right: 10px;
}
</style>
