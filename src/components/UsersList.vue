<template>
  <!-- tag="ul" is similar to <ul> element -->
  <transition-group tag="ul" name="user-list">
    <li v-for="user in users" :key="user.id" @click="removeUser(user.id)">
      {{ user.name }}
    </li>
  </transition-group>
  <div>
    <input type="text" ref="userNameInput" />
    <button @click="addUser">Add User</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nextId: 6,
      users: [
        { id: 1, name: 'David' },
        { id: 2, name: 'Thorin' },
        { id: 3, name: 'Dwaylin' },
        { id: 4, name: 'Balin' },
        { id: 5, name: 'Gandalf' }
      ]
    };
  },
  methods: {
    addUser() {
      const enteredUserName = this.$refs.userNameInput.value;
      const newId = this.nextId++;
      const newUser = { id: +newId, name: enteredUserName };
      this.users.unshift(newUser);
      console.log('Current ID: ' + this.nextId);
    },
    removeUser(userId) {
      console.log(userId);
      this.users = this.users.filter(usr => usr.id !== userId);
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
li {
  border: 1px solid #ccc;
  padding: 1rem;
  text-align: center;
}

.user-list-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}

.user-list-enter-active {
  transition: all 1s ease-out;
}

.user-list-enter-to,
.user-list-leave-from {
  opacity: 1;
  transform: translateX(0);
}

.user-list-leave-active {
  transition: all 1s ease-out;
  position: absolute;
}

.user-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.user-list-move {
  transition: transform 0.8s ease;
}
</style>
