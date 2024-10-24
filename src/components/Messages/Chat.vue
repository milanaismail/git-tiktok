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

function addMessage(newMessage) {
    console.log('Received message:', newMessage);

    if (!newMessage || !newMessage.user || !newMessage.text) {
        console.error('Invalid message data:', newMessage);
        return;
    }

    const messageToSend = {
        message: {
            user: newMessage.user,
            text: newMessage.text,
        }
    };

    console.log('Sending message:', messageToSend);

    // Add the new message to the local messages array (append to the end)
    state.messages.push(newMessage);

    // Send the new message to the API
    fetch('https://mongodb-ig7g.onrender.com/api/v1/messages', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(messageToSend),
    })
    .then(res => {
        if (!res.ok) {
            throw new Error(`HTTP error! status: ${res.status}`);
        }
        return res.json();
    })
    .then(data => {
        console.log('Message saved:', data);
    })
    .catch(err => {
        console.error('Error sending message:', err);
    });
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
