<script setup lang="ts">

const props = defineProps({
    entryName: String,
    logoName: String
})

const logoPath =  "/src/assets/" + props.logoName

</script>

<template>
    <div class="entry-body">
        <img class="icon" :src=logoPath alt="">
        <span class="entry-name-text">{{ entryName }}</span>
    </div>
</template>

<style>

.entry-body {
    display: inline-block;

    vertical-align: middle;
    text-align: center;

    height: 250px;
    width: 500px;

    border: 1px solid black;
    border-radius: 25px;

    box-shadow: 2px 2px 5px #000;
}

.icon {
    vertical-align: middle;
    height: 100px;
}

.entry-name-text {
    display: block;
    font-family: "KaiTi", cursive, serif, sans-serif;
    font-weight: bold;
    font-size: 30px;
}

</style>