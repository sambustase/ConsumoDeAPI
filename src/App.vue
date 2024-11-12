<template>
  <div id="app">
    <Chat :users="users" @sendMessage="addMessage" :messages="messages" />
  </div>
</template>

<script>
import axios from 'axios';
import Chat from './components/Chat.vue';

export default {
  name: 'App',
  components: { Chat },
  data() {
    return {
      users: [],
      messages: []
    };
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get('https://randomuser.me/api/?results=2');
        this.users = response.data.results.map((user) => ({
          name: `${user.name.first} ${user.name.last}`,
          picture: user.picture.thumbnail
        }));
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
    addMessage(message) {
      this.messages.push(message);
    }
  },
  created() {
    this.fetchUsers();
  }
};
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  padding: 20px;
}
</style>