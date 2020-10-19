<template>
  <main>
    <div class="contacts-list">
      <ContactListItem
        v-for="(contact, index) in contacts"
        v-bind:key="index"
        :contact="contact"
        v-on="$listeners"
      />
    </div>
  </main>
</template>

<script>
import ContactListItem from "./ContactListItem";
export default {
  name: "contacts-list-item",
  components: {
    ContactListItem,
  },
  props: {
    contacts: Array,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.contacts-list {
  max-width: 400px;
  padding: 20px;
  margin: 0 auto;
}
</style>
