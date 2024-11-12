<template>
    <div class="chat-container">
      <div class="chat-box">
        <div v-for="(msg, index) in messages" :key="index">
          <Message :msg="msg" />
        </div>
      </div>
      <div class="user-inputs">
        <div v-for="(user, index) in users" :key="index" class="user-box">
          <img :src="user.picture" alt="User Avatar" class="avatar" />
          <p>{{ user.name }}</p>
          <input type="text" v-model="newMessages[index]" placeholder="Escribe un mensaje" />
          <button @click="sendMessage(index)">Enviar</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Message from './Message.vue';
  
  export default {
    name: 'Chat',
    components: { Message },
    props: ['users', 'messages'],
    data() {
      return {
        newMessages: ['', ''] 
      };
    },
    methods: {
      sendMessage(index) {
        if (this.newMessages[index].trim()) {
          this.$emit('sendMessage', { text: this.newMessages[index], owner: this.users[index].name });
          this.newMessages[index] = ''; 
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .chat-container {
    display: flex;
    flex-direction: column;
    width: 60%;
  }
  
  .chat-box {
    flex: 1;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 10px;
    margin-bottom: 20px;
    max-height: 300px;
    overflow-y: auto;
    background-color: #f9f9f9;
  }
  
  .user-inputs {
    display: flex;
    justify-content: space-between;
  }
  
  .user-box {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .avatar {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin-bottom: 5px;
  }
  
  input {
    margin-bottom: 5px;
  }
  
  button {
    cursor: pointer;
  }
  </style>