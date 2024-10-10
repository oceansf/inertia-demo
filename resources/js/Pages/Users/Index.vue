<script setup>
import { ref, watch } from "vue";
import Pagination from "../../Shared/Pagination.vue";
import { Link, router } from "@inertiajs/vue3";
import debounce from 'lodash/debounce';

let props = defineProps({ users: Object, filters: Object, can: Object });

let search = ref(props.filters.search);

watch(search,
    debounce(function (value) {
        router.get(
            "/users",
            {search: value},
            {preserveState: true, replace: true}
        )
    }, 300)
);
</script>

<template>
    <Head title="Users" />
    <div class="flex justify-between">
        <div class="flex items-center">
        <h1 class="text-3xl">Users</h1>
        <Link v-if="can.createUser" href="/users/create" class="text-blue-500 text-sm ml-3">New User</Link>
        </div>
        <input
            v-model="search"
            type="text"
            placeholder="Search..."
            class="border px-2 rounded-lg"
        />
    </div>
    <div class="mt-4">
        <ul role="list" class="divide-y divide-gray-100">
            <li
                v-for="user in users.data"
                :key="user.id"
                class="flex justify-between gap-x-6 py-5"
            >
                <div class="flex min-w-0 gap-x-4">
                    <div class="min-w-0 flex-auto">
                        <p
                            class="text-sm font-semibold leading-6 text-gray-900"
                        >
                            {{ user.name }}
                        </p>
                    </div>
                </div>
                <div class="hidden shrink-0 sm:flex sm:flex-col sm:items-end">
                    <Link
                        v-if="user.can.edit"
                        href="`/users/${user.id}/edit`"
                        class="text-indigo-600 hover:text-indigo-900 font-semibold"
                        >Edit</Link
                    >
                </div>
            </li>
        </ul>
        <Pagination :links="users.links" class="mt-4" />
    </div>
</template>
