<template>
    <NuxtLink class="underline font-medium" :href="firstLesson.path">
        Go for the first lesson
    </NuxtLink>
</template>


<script setup>
const firstLesson = useFirstLesson();
console.log(firstLesson);
</script>
