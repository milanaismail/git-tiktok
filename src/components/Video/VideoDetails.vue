<script setup>
    let name = 'Milana';
    let image = 'src/assets/me.jpg';
    const props = defineProps({
        title: String });
</script>

<template>
    <div class="video__detail">
        <img :src="image" alt="profile picture">
        <a href="" class="username">
            <p>{{ name }}</p>
        </a>
    </div>
            <h2>{{ title }}</h2>
</template>

<style scoped>
.video__detail {
    display: flex;
    gap: 10px;
    align-items: center;
}
img {
    width: 50px;
    height: 50px;
    border-radius: 50%;
}
</style>
