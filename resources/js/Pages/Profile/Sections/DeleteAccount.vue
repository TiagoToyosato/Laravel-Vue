<script setup>
import Container from "../../../Components/Container.vue";
import Title from "../../../Components/Title.vue";
import InputField from "../../../Components/InputField.vue";
import PrimaryBtn from "../../../Components/PrimaryBtn.vue";
import ErrorMessages from "../../../Components/ErrorMessages.vue";
import { useForm } from "@inertiajs/vue3";
import { ref } from "vue";

const showConfirmPassword = ref(false);

const form = useForm({
    password: "",
});

const submit = () => {
    form.delete(route("profile.destroy"), {
        preserveScroll: true,
        onFinish: () => {
            form.reset();
        },
    });
};
</script>

<template>
    <Container class="mb-6">
        <div class="mb-6">
            <Title>Delete Account</Title>
            <p>
                Once your account is deleted, all of its resources data will be
                permanently deleted. This action cannot be undone.
            </p>
        </div>

        <ErrorMessages :errors="form.errors" />

        <div v-if="showConfirmPassword" class="mb-6" @submit.prevent="submit">
            <form class="flex items-end gap-4">
                <inputField
                    label="Confirm Password"
                    icon="key"
                    class="w-1/2"
                    type="password"
                    v-model="form.password"
                />

                <!-- USAR PARA TENTAR ADICIONAR UM DIGITE APAGAR PARA REALMENTE APAGAR -->
                <!-- <inputField
                label="Email"
                icon="at"
                class="w-1/2"
                v-model="form.email"
            /> -->

                <PrimaryBtn :disabled="form.processing">Save</PrimaryBtn>

                <button
                    @click="showConfirmPassword = false"
                    class="text-indigo-500 font-medium underline dark:text-indigo-400"
                >
                    Cancel
                </button>
            </form>
        </div>

        <button
            v-if="!showConfirmPassword"
            @click="showConfirmPassword = true"
            class="px-6 py-2 rounded-lg bg-red-500 text-white hover:bg-red-600 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-opacity-50 transition duration-150 ease-in-out flex items-center"
        >
            <i class="fa-solid fa-triangle-exclamation mr-2"></i>
            Delete Account
        </button>
    </Container>
</template>
