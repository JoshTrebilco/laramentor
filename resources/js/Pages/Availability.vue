<script setup>
import TimeInput from '@/Components/TimeInput.vue';
import Checkbox from '@/Components/Checkbox.vue';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue';

const daysInWeek = ref([
    { name: 'Sunday', active: false, startTime: '9:00 AM', endTime: '5:00 PM'},
    { name: 'Monday', active: true, startTime: '9:00 AM', endTime: '5:00 PM'},
    { name: 'Tuesday', active: true, startTime: '9:00 AM', endTime: '5:00 PM'},
    { name: 'Wednesday', active: true, startTime: '9:00 AM', endTime: '5:00 PM'},
    { name: 'Thursday', active: true, startTime: '9:00 AM', endTime: '5:00 PM'},
    { name: 'Friday', active: true, startTime: '9:00 AM', endTime: '5:00 PM'},
    { name: 'Saturday', active: false, startTime: '9:00 AM', endTime: '5:00 PM'},
])

</script>

<template>
    <Head title="Availability" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Availability</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-gray-800 shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900 dark:text-gray-100">

                        <div v-for="day in daysInWeek" class="flex items-center">
                            <!-- checkbox to set day to active -->
                            <div class="flex w-40 h-10 items-center">
                                <Checkbox v-model:checked="day.active" />
                                <span class="ml-3">{{ day.name }}</span>
                            </div>


                            <!-- if active, show time dropdowns -->
                            <div v-if="day.active" class="flex">
                                <TimeInput v-model="day.startTime" :endTime="day.endTime" />
                                <TimeInput v-model="day.endTime" :startTime="day.startTime" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
