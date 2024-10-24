<script setup>
// Get messages from MongoDB
import { defineProps } from 'vue';

const props = defineProps({
  messages: {
    type: Array,
    required: true
  }
});
</script>

<template>
    <div class="comments">
        <ul>
            <li v-for="(message, index) in props.messages" :key="index">
                <strong><p>{{ message.user }}</p></strong>
                <p>{{ message.text }}</p>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.comments {
    margin-top: 20px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
    height: 300px;
    overflow-y: scroll;
}
.comments ul {
    list-style-type: none;
    padding: 0;
}
.comments li {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #fff;
}
</style>
