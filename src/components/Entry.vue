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

    box-shadow: 3px 3px 5px #000;
}

.icon {
    padding-top: 25px;
    vertical-align: middle;
    height: 125px;
}

.entry-name-text {
    display: block;
    font-family: "KaiTi", cursive, serif, sans-serif;
    font-weight: bold;
    font-size: 50px;
    line-height: 100px;
}
