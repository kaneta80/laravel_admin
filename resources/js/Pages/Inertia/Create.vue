<script setup>
import { reactive } from "vue";
import { Inertia } from "@inertiajs/inertia";

defineProps({
    errors: Object,
});

const form = reactive({
    title: null,
    content: null,
});

const submitfunction = () => {
    Inertia.post("/inertia", form);
};
</script>

<template>
    <form @submit.prevent="submitfunction">
        <!--@submit.preventでページ全てを読み込みのを避けている-->
        <input type="text" name="title" v-model="form.title" /><br />
        <div v-if="errors.title">{{ errors.title }}</div>
        <br />
        <input type="text" name="content" v-model="form.content" /><br />
        <div v-if="errors.content">{{ errors.content }}</div>
        <br />
        <button>送信</button>
        <!--このボタンをクリックするとフォームタグ内の@submitがはしる -->
    </form>
</template>
