<script setup>
import { reactive, onMounted } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

const state = reactive({
  messages: []
});

async function fetchMessages() {
  try {
    const response = await fetch('https://mongodb-ig7g.onrender.com/api/v1/messages');
    const data = await response.json();
    state.messages = data.data.messages;
  } catch (error) {
    console.error('Error fetching messages:', error);
  }
}

// Function to add the new message to the messages list
function addMessage(newMessage) {
  state.messages.push(newMessage);
}

onMounted(() => {
  fetchMessages(); // Fetch messages when the component mounts
});
</script>

<template>
   <ChatMessages :messages="state.messages" />
   <ChatForm @sendMessage="addMessage" />
</template>

<style scoped>

</style>
