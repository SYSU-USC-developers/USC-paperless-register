<script setup lang="ts">

defineProps<{ entryName: string }>();

</script>

<template>
    <div class="entry-body">
        <img src="../assets/umbrella.png">
        <h2> {{ entryName }} </h2>
    </div>
</template>