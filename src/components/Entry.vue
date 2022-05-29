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

.icon {
    vertical-align: middle;
}

.entry-name-text {
    font-family: "KaiTi", cursive, serif, sans-serif;
    font-weight: bold;
    font-size: 30px;
}

</style>