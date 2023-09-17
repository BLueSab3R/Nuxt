<template>
    <div class="flex flex-col items-center justify-center prose w-full max-w-2xl h-9">
        <h1 class="text-center mt-10">Log into {{ title }}</h1>
        <button @click="login" class="bg-blue-500  text-white font-bold py-2 px-4 rounded">
            Log in with GitHub
        </button>
    </div>
</template>



<script setup>
const { title } = useCourse();
const supabase = useSupabaseClient();
const login = async () => {
    const { error, data } = await supabase.auth.signInWithOAuth({
        provider: 'github',
    });
    if (error) {
        console.log(error);
    }
    console.log(data);
}
</script>