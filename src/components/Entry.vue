<script setup lang="ts">

defineProps<{ entryName: string }>();

</script>

<template>
    <div class="entry-body">
        <img class="icon" src="../assets/umbrella.png">
        <span class="entry-name-text">{{ entryName }}</span>
    </div>
</template>

<style>

.entry-body {
    height: 100px;
    width: 250px;

    border: 1px solid black;
    border-radius: 25px;

    box-shadow: 2px 2px 5px #000;
}

.icon {
    vertical-align: middle;
    height: 100px;
}

.entry-name-text {
    font-family: "KaiTi", cursive, serif, sans-serif;
    font-weight: bold;
    font-size: 30px;
}

</style>