<template>
    <div>
        <p class="mt-0 uppercase font-bold text-slate-400 mb-1">
            Lesson {{ chapter.number }} - {{ lesson.number }}
        </p>
        <h2 class="my-0">{{ lesson.title }}</h2>
        <div class="flex space-x-4 mt-2 mb-8">
            <NuxtLink v-if="lesson.sourceUrl" class="font-normal text-md text-gray-500" :to="lesson.sourceUrl">
                Download SourceCode
            </NuxtLink>
            <NuxtLink v-if="lesson.downloadUrl" class="font-normal text-md text-gray-500" :to="lesson.downloadUrl">
                Download Video
            </NuxtLink>
        </div>
        <VideoPlayer v-if:="lesson.videoId" :videoId="lesson.videoId" />
        <p class="mb-10">{{ lesson.text }}</p>
        <ClientOnly>
            <LessonCompleteButton :model-value="isLessonComplete" @update:model-value="toggleComplete" />
        </ClientOnly>
    </div>
</template>



<script setup>

definePageMeta({
    middleware: [
        function ({ params }, from) {
            const course = useCourse();
            const chapter = course.chapters.find(
                (chapter) => chapter.slug === params.chapterSlug
            )
            if (!chapter) {
                return createError({
                    statusCode: 404,
                    message: 'Chapter is not found',
                });
            }

            const lesson = chapter.lessons.find(
                (lesson) => lesson.slug === params.lessonSlug
            )
            if (!lesson) {
                return abortNavigation(
                    createError({
                        statusCode: 404,
                        message: 'Lesson is not found',
                    })

                );
            }
        },
        'auth'
    ]
});

const route = useRoute();
const course = useCourse();
// if (route.params.lessonSlug === '2-typescript-in-vue-components') {
//     route.params.paramsthatdontexistwhoops.captilizeIsNotTheMethod();
// }


const chapter = computed(() => {
    return course.chapters.find(
        (chapter) => chapter.slug === route.params.chapterSlug
    );
});


const lesson = computed(() => {
    return chapter.value.lessons.find(
        (lesson) => lesson.slug === route.params.lessonSlug
    );
})


const title = computed(() => {
    return `${lesson.value.title}`;
})
useHead({
    title: title
})
const progress = useLocalStorage('progress', []);
const isLessonComplete = computed(() => {
    if (!progress.value[chapter.value.number - 1]) {
        return false;
    }
    if (!progress.value[chapter.value.number - 1][
        lesson.value.number - 1]) {
        return false;
    }
    return progress.value[chapter.value.number - 1][
        lesson.value.number - 1
    ];
});
const toggleComplete = () => {
    if (!progress.value[chapter.value.number - 1]) {
        progress.value[chapter.value.number - 1] = [];
    }
    progress.value[chapter.value.number - 1][
        lesson.value.number - 1
    ] = !isLessonComplete.value;
}

</script>   

