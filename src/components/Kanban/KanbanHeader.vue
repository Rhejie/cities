<template>
    <div class="">
        <div class="flex px-2 pt-4 sm:px-6">
            <div class="flex min-w-0 flex-1">
                <div
                    class="min-w-0 flex-1 px-2 md:grid md:grid-cols-2 md:gap-4"
                >
                    <p
                        class="truncate inline-flex text-sm font-medium text-gray-600"
                    >
                        <RectangleGroupIcon
                            class="h-5 w-5 text-gray-500 mr-2"
                            aria-hidden="true"
                        />
                        {{ title }}
                    </p>
                </div>
            </div>
            <div class="bg-white px-1 rounded-lg flex" v-if="showButtons">
                <ChatBubbleLeftEllipsisIcon
                    class="h-5 w-5 text-gray-400 mr-2"
                    aria-hidden="true"
                />
                <PlusIcon
                    class="h-5 w-5 text-gray-400 mr-2"
                    aria-hidden="true"
                />
                <Bars4Icon class="h-5 w-5 text-gray-400" aria-hidden="true" />
            </div>
        </div>
    </div>
</template>
<script setup>
import {
    Bars4Icon,
    ChatBubbleLeftEllipsisIcon,
    PlusIcon,
    RectangleGroupIcon,
} from "@heroicons/vue/24/outline";
import { defineProps, computed } from "vue";

const props = defineProps({
    title: {
        type: String,
        default: null,
    },
    showButtons: {
        type: Boolean,
        default: false,
    }
});

const title = computed(() => props.title);
const showButtons = computed(() => props.showButtons)
</script>
