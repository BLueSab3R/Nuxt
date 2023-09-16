<template>
    <div class="prose flex justify-center ">
        <div>
            <h1>404</h1>
            <p>Page does not exist</p>
            <p>
                <strong>{{ error.message }}</strong>
            </p>
        </div>
    </div>
</template>


<script setup>
const error = useError();
</script>
