<script setup>
import { ref } from 'vue';

const emit = defineEmits(['sendMessage']);


let name = ref('User'); 
let messageText = ref('');

function doit(){
    if (messageText.value.trim() !== "") {
        const newMessage = {
            user: name.value,
            text: messageText.value
        };
        
        emit('sendMessage', newMessage);
    }
}

</script>

<template>
    <div class="form">
        <div class="comment-section">
            <label for="name">{{ name }}:</label>
            <input v-model="messageText" type="text" placeholder="Type your message here...">
            <button @click.prevent="doit">Send</button>
        </div>
    </div>
</template>

<style scoped>
    .form{
        display: flex;
        gap: 10px;
        flex-direction: column;
        display: flex;
    }
    input{
        flex: 1;
        padding: 10px;
        font-size: 1rem;
    }

</style>
