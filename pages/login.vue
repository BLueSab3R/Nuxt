<template>
    <div class="flex flex-col items-center justify-center prose w-full max-w-2xl h-9">
        <h1 class="text-center mt-10">Log into {{ title }}</h1>
        <button class="bg-blue-500  text-white font-bold py-2 px-4 rounded">
            Log in with GitHub
        </button>
    </div>
</template>



<script setup>
const { title } = useCourse();
</script>