<template>
  <div class="message" :class="{ 'user-one': msg.owner === ownerOne, 'user-two': msg.owner !== ownerOne }">
    <strong>{{ msg.owner }}:</strong> {{ msg.text }}
  </div>
</template>

<script>
export default {
  name: 'Message',
  props: ['msg'],
  computed: {
    ownerOne() {
      return this.$parent.users[0].name; 
    }
  }
};
</script>

<style scoped>
.message {
  padding: 10px;
  margin: 5px;
  border-radius: 5px;
}

.user-one {
  background-color: #e1f5fe;
  text-align: left;
}

.user-two {
  background-color: #ffebee;
  text-align: right;
}
</style>