<template>
    <div>
        <div class="prose mb-12">
            <h1>
                <span class='font-medium'>
                    <span class="font-bold">{{ title }}</span>
                </span>
            </h1>
        </div>
        <div class="flex flex-row justify-center flex-grow">
            <div class="prose mr-4 p-8 bg-white font-bold  rounded-md min-w-[20ch] flex flex-col">
                <h3 class="text-xl font-bold">
                    Chapters
                </h3>
                <div class="mb-4 flex flex-col  " v-for="chapter in chapters" :key='chapter.slug'>
                    <h4 class="mt-2">{{ chapter.title }}</h4>
                    <NuxtLink v-for="(lesson, index) in chapter.lessons" :key='lesson.slug' :to="lesson.path"
                        class="flex no-underline hover:tex-tet cursor-pointer flex-row space-x-1 prose-sm font-normal py-1">
                        <span class="text-gray-500">{{ index + 1 }}.</span>
                        <span>{{ lesson.title }}</span>
                    </NuxtLink>

                </div>
            </div>

            <div class="prose p-12 bg-white rounded-md w-[80ch]">
                <NuxtErrorBoundary>
                    <NuxtPage />
                    <template #error="{ error }">
                        <p>
                            Oh, something wrong with the lesson:
                            <code>{{ error }}</code>
                        </p>
                        <p>
                            <button class="hover:cursor-pointer bg-gray-500 text-white font-bold"
                                @click="resetError(error)">
                                Reset
                            </button>
                        </p>
                    </template>
                </NuxtErrorBoundary>
            </div>
        </div>
    </div>
</template>


<script setup>

const { chapters, title } = useCourse();

const resetError = async (error) => {
    error.value = null;
    await navigateTo('/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3')
}

</script>


<style scoped>
.router-link-active {
    color: blue;
}
</style>