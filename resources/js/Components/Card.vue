<script setup>
import { router } from "@inertiajs/vue3";

const params = route().params;

defineProps({
    listing: Object,
});

const selectUser = (id) => {
    router.get(route("home"), {
        search: params.search,
        user_id: id,
        tag: params.tag,
    });
};

const selectTag = (tag) => {
    router.get(route("home"), {
        search: params.search,
        user_id: params.user_id,
        tag: tag,
    });
};
</script>

<template>
    <div
        class="bg-white rounded-lg shadow-lg overflow-hidden dark:bg-slate-800 h-full flex flex-col justify-between"
    >
        <div>
            <!-- IMAGE -->
            <Link href="" class="">
                <img
                    :src="
                        listing.image
                            ? `/storage/${listing.image}`
                            : '/storage/images/listing/default.jpeg'
                    "
                    class="w-full h-48 bg-slate-300 object-cover object-center"
                    alt=""
            /></Link>

            <!-- TITLE & USER -->
            <div class="p-4">
                <h3 class="font-bold text-xl mb-2">
                    {{ listing.title.substring(0, 40) }}...
                </h3>

                <p>
                    Listed on
                    {{ new Date(listing.created_at).toLocaleDateString() }} by
                    <button
                        class="text-link"
                        @click="selectUser(listing.user.id)"
                    >
                        {{ listing.user.name }}
                    </button>
                </p>
            </div>
        </div>
        <!-- TAGS -->
        <div v-if="listing.tags" class="flex items-center gap-3 px-4 pb-4">
            <div v-for="tag in listing.tags.split(',')" :key="tag">
                <button
                    class="bg-slate-500 text-white px-2 py-px rounded-full hover:bg-slate-700 dark:hover:bg-slate-900"
                    @click="selectTag(tag)"
                >
                    {{ tag }}
                </button>
            </div>
        </div>
    </div>
</template>
