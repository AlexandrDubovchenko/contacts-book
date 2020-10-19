<template>
  <div class="home">
    <ContactsList v-on="$listeners" v-bind:contacts="contacts" />
  </div>
</template>

<script>
import ContactsList from "../components/ContactsList.vue";
export default {
  name: "app",
  components: {
    ContactsList,
  },
  props: {
    contacts: Array,
  },
};
</script>
