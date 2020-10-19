<template>
  <div id="app">
    <Header @revert="revertHandler" @toggle-add-form="toggleAddForm" />
    <div id="nav"><router-link class="btn btn_home" v-if="!isHome" to="/">Home</router-link></div>
    <main>
      <router-view
        @change-contact="changeContact"
        @change-data="changeData"
        @add-data="addContactData"
        @delete-data="deleteContactData"
        @delete-contact="deleteContact"
        v-bind:contacts="contacts"
      />
    </main>
    <div v-if="addFormVisible" class="add_form_container">
      <AddContactForm
        @toggle-add-form="toggleAddForm"
        @add-contact="addContact"
      />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import AddContactForm from "./components/AddContactForm";
import "./styles/styles.css";
export default {
  name: "app",
  components: {
    Header,
    AddContactForm,
  },
  data() {
    return {
      addFormVisible: false,
      isStepBack: false,
      contacts: [
        {
          id: 0,
          name: "Contact Name",
          avatar:
            "https://okeygeek.ru/wp-content/uploads/2020/03/no_avatar.png",
          data: [
            {
              tel: "+38067456",
            },
            {
              email: "test@gmail.com",
            },
          ],
        },
        {
          id: 1,
          name: "Contact Name@",
          avatar:
            "https://okeygeek.ru/wp-content/uploads/2020/03/no_avatar.png",
          data: [
            {
              tel: "+38067456",
            },
            {
              email: "test@gmail.com",
            },
          ],
        },
      ],
      prevContacts: [],
    };
  },
  computed: {
    isHome: function () {
      return this.$route.name === "Home";
    },
  },
  methods: {
    addContactData: function (newData) {
      this.isStepBack = true;
      this.prevContacts = this.contacts.map((contact) => ({...contact, data: [...contact.data]}));
      this.contacts
        .find((contact) => contact.id === newData.id)
        .data.push({
          [newData.title]: newData.value,
        });
    },
    deleteContactData: function (data) {
      this.isStepBack = true;
      this.prevContacts = this.contacts.map((contact) => ({...contact, data: [...contact.data]}));
      this.contacts.find(
        (contact) => contact.id === data.id
      ).data = this.contacts
        .find((contact) => contact.id === data.id)
        .data.filter((d, index) => index !== data.index);
    },
    changeData: function (data) {
      this.isStepBack = true;
      this.prevContacts = this.contacts.map((contact) => ({...contact, data: [...contact.data]}));
      this.$set(
        this.contacts.find((contact) => contact.id === data.id).data,
        data.index,
        data.value
      );
    },
    changeContact: function (data) {
      this.isStepBack = true;
      this.prevContacts = this.contacts.map((contact) => ({...contact, data: [...contact.data]}));
      this.$set(
        this.contacts.find((contact) => contact.id === data.id),
        ["name"],
        data.name
      );
      this.$set(
        this.contacts.find((contact) => contact.id === data.id),
        ["avatar"],
        data.avatar
      );
    },
    toggleAddForm: function () {
      this.addFormVisible = !this.addFormVisible;
    },
    addContact: function (contact) {
      this.isStepBack = true;
      this.prevContacts = this.contacts.map((contact) => ({...contact, data: [...contact.data]}));
      this.contacts.push(contact);
      this.toggleAddForm();
    },
    deleteContact: function (id) {
      this.isStepBack = true;
      this.prevContacts = this.contacts.map((contact) => ({...contact, data: [...contact.data]}));
      this.contacts = this.contacts.filter((contact) => contact.id !== id);
    },
    revertHandler: function () {
      this.contacts = this.prevContacts;
      this.isStepBack = false;
    },
  },
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

main {
  max-width: 700px;
  margin: 0 auto;
}

#nav {
  padding: 30px;
}
.add_form_container {
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
  width: 100vw;
  height: 100vh;
}
.btn_home {
  background: #d81b60;
  color: #fff;
}
</style>
