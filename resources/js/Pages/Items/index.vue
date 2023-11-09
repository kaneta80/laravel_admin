<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head } from "@inertiajs/vue3";
import { Link } from "@inertiajs/inertia-vue3";
import FlashMessage from "@/Components/FlashMessage.vue";
import {ref} from 'vue';

defineProps({
    items:Array,
    errors:Object
})

const search = ref("")

const searchCustomers = () => { 
 Inertia.get(route('customers.index', { search: search.value })) 
}
</script>

<template>
    <Head title="商品一覧" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                商品一覧
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <section class="text-gray-600 body-font">
                        <div class="container px-5 py-8 my-auto">
                            <FlashMessage />
                            <div class="flex pl-4 my-4 lg:w-2/3 w-full mx-auto">
                              <div>
                                <input type="text" name="search" v-model="search">
                                <button class="bg-blue-300 text-white py-2 px-2" @click="searchCustomers">検索</button>
                              </div>
                              <Link as="button" :href="route('customers.create')" class="flex ml-auto text-white bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded">顧客登録</Link>
                            </div>
                            <div class="lg:w-2/3 w-full mx-auto overflow-auto">
                            <table class="table-auto w-full text-left whitespace-no-wrap">
                                <thead>
                                <tr>
                                    
                                    <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100 rounded-tl rounded-bl">ID</th>
                                    <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100">商品名</th>
                                    <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100">価格</th>
                                    <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100">ステータス</th>
                                </tr>
                                </thead>
                                <tbody>
                                <tr v-for="item in items" :key="item.id">
                                    <td class="px-4 py-3 border-b-2 border-gray-200">
                                        <Link class="text-blue-400" :href="route('items.show' , {item:item.id})">{{ item.id }}</Link>
                                    </td>
                                    <td class="px-4 py-3 border-b-2 border-gray-200">{{ item.name }}</td>
                                    <td class="px-4 py-3 border-b-2 border-gray-200">{{ item.price }}</td>
                                    <td class="px-4 py-3 border-b-2 border-gray-200 text-lg text-gray-900">
                                        <span v-if="item.is_selling===1">販売中</span>
                                        <span v-if="item.is_selling===0">停止中</span>
                                    </td>
                                </tr>
                                </tbody>
                            </table>
                            </div>
                        </div>
                        </section>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
