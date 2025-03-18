<script setup>
defineProps({
    errors: {
        type: Object,
    },
});
</script>

<template>
    <div class="mb-4" v-if="Object.keys(errors).length > 0">
        <p class="text-sm text-red-500">Something went wrong!</p>
        <ul class="ml-4 list-disc list-inside">
            <li
                v-for="(error, index) in errors"
                :key="index"
                class="text-sm text-red-500"
            >
                {{ error }}
            </li>
        </ul>
    </div>
</template>
