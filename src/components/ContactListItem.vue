<template>
  <div class="contact-item">
    <router-link
      class="contact-info"
      :to="{ name: 'Contact', params: { id: contact.id } }"
    >
      <div class="avatar">
        <img :src="contact.avatar" alt="" />
      </div>
      <div class="name">
        <span>{{ contact.name }}</span>
      </div>
    </router-link>
    <button @click="deleteContact(contact.id)" class="btn btn-delete">
      Delete
    </button>
  </div>
</template>

<script>
export default {
  name: "conact-list-item",
  props: {
    contact: Object,
  },
  methods: {
    deleteContact: function (id) {
      if (confirm("Are you sure?")) {
        this.$emit("delete-contact", id);
      }
    },
  },
};
</script>

<style scoped>
.contact-item {
  display: flex;
  align-items: center;
  font-size: 20px;
  letter-spacing: 2px;
  cursor: pointer;
  padding: 0 10px 0 0;
  justify-content: space-between;
  user-select: none;
}
.contact-info {
  display: flex;
  flex: 1;
  align-items: center;
  margin-right: 15px;
}
.contact-info:hover {
  background-color: #f2f2f2;
}
.contact-info:active {
  background: #d3f3f3;
}
.avatar img {
  border-radius: 50%;
  width: 36px;
  height: 36px;
  margin-right: 2rem;
}
.btn-delete {
  background-color: #d81b60;
  color: #fff;
  border-radius: 4px;
}
.btn-delete:active {
  color: #d81b49;
  background-color: #fff;
}
</style>
