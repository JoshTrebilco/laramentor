<script setup>
import { ref, computed } from 'vue';
import { CheckIcon, ChevronUpDownIcon } from '@heroicons/vue/20/solid'
import { Listbox, ListboxButton, ListboxOptions, ListboxOption } from '@headlessui/vue'

const props = defineProps({
    modelValue: {
        type: String,
        required: true,
    },
    startTime: {
        type: String,
        required: false,
    },
    endTime: {
        type: String,
        required: false,
    },
});

const emit = defineEmits(['update:modelValue']);

const times = ref([
    '12:00 AM',
    '12:15 AM',
    '12:30 AM',
    '12:45 AM',
    '1:00 AM',
    '1:15 AM',
    '1:30 AM',
    '1:45 AM',
    '2:00 AM',
    '2:15 AM',
    '2:30 AM',
    '2:45 AM',
    '3:00 AM',
    '3:15 AM',
    '3:30 AM',
    '3:45 AM',
    '4:00 AM',
    '4:15 AM',
    '4:30 AM',
    '4:45 AM',
    '5:00 AM',
    '5:15 AM',
    '5:30 AM',
    '5:45 AM',
    '6:00 AM',
    '6:15 AM',
    '6:30 AM',
    '6:45 AM',
    '7:00 AM',
    '7:15 AM',
    '7:30 AM',
    '7:45 AM',
    '8:00 AM',
    '8:15 AM',
    '8:30 AM',
    '8:45 AM',
    '9:00 AM',
    '9:15 AM',
    '9:30 AM',
    '9:45 AM',
    '10:00 AM',
    '10:15 AM',
    '10:30 AM',
    '10:45 AM',
    '11:00 AM',
    '11:15 AM',
    '11:30 AM',
    '11:45 AM',
    '12:00 PM',
    '12:15 PM',
    '12:30 PM',
    '12:45 PM',
    '1:00 PM',
    '1:15 PM',
    '1:30 PM',
    '1:45 PM',
    '2:00 PM',
    '2:15 PM',
    '2:30 PM',
    '2:45 PM',
    '3:00 PM',
    '3:15 PM',
    '3:30 PM',
    '3:45 PM',
    '4:00 PM',
    '4:15 PM',
    '4:30 PM',
    '4:45 PM',
    '5:00 PM',
    '5:15 PM',
    '5:30 PM',
    '5:45 PM',
    '6:00 PM',
    '6:15 PM',
    '6:30 PM',
    '6:45 PM',
    '7:00 PM',
    '7:15 PM',
    '7:30 PM',
    '7:45 PM',
    '8:00 PM',
    '8:15 PM',
    '8:30 PM',
    '8:45 PM',
    '9:00 PM',
    '9:15 PM',
    '9:30 PM',
    '9:45 PM',
    '10:00 PM',
    '10:15 PM',
    '10:30 PM',
    '10:45 PM',
    '11:00 PM',
    '11:15 PM',
    '11:30 PM',
    '11:45 PM',
    '11:59 PM',
])

const filteredTimes = computed(() => {
    let start = 0;
    let end = times.value.length;

    if (props.startTime) {
        start = times.value.indexOf(props.startTime) + 1;
    }

    if (props.endTime) {
        end = times.value.indexOf(props.endTime);
    }

    return times.value.slice(start, end);
});

</script>

<template>
    <Listbox
        as="div"
        :modelValue="modelValue" @update:modelValue="value => emit('update:modelValue', value)"
        >
        <div class="relative w-36">
            <ListboxButton class="block border border-gray-300 dark:border-gray-700 dark:bg-gray-900 dark:text-gray-300 rounded-md shadow-sm w-full relative py-1 pl-3 pr-10 text-left">
                <span class="block truncate">{{ modelValue }}</span>
                <span
                    class="pointer-events-none absolute inset-y-0 right-0 flex items-center pr-2"
                >
                    <ChevronUpDownIcon
                    class="h-5 w-5 text-gray-400"
                    aria-hidden="true"
                    />
                </span>
            </ListboxButton>

            <ListboxOptions
                class="absolute z-40 mt-1 max-h-60 w-full overflow-auto rounded-md bg-white dark:bg-gray-800 py-1 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none">
                <ListboxOption v-for="time in filteredTimes" :key="time" :value="time" as="template"
                    v-slot="{ active, selected }">
                    <li
                        :class="['relative cursor-default select-none py-2 pl-3 pr-9', active ? 'bg-indigo-600 text-white' : 'text-gray-900 dark:text-gray-300']">
                        <span :class="['block truncate', selected && 'font-semibold']">
                            {{ time }}
                        </span>

                        <span v-if="selected"
                            :class="['absolute inset-y-0 right-0 flex items-center pr-4', active ? 'text-white' : 'text-indigo-600']">
                            <CheckIcon class="h-5 w-5" aria-hidden="true" />
                        </span>
                    </li>
                </ListboxOption>
            </ListboxOptions>
        </div>
    </Listbox>
</template>
