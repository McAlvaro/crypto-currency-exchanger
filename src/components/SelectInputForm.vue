<script setup>

defineProps(["label", "options"])

defineEmits(['getPrice']);

const currencyAmount = defineModel('currencyAmount');
const currency = defineModel('currency');

</script>
<template>

    <div class="flex flex-col justify-between p-6 leading-normal">
        <p v-text="label"></p>
        <div class="flex">
            <label for="search-dropdown" class="mb-2 text-sm font-medium text-blue-500 sr-only">Currency</label>
            <div class="relative">
                <input @input="$emit('getPrice')" v-model="currencyAmount" type="number" id="search-dropdown"
                    class="block w-36 p-3 z-20 text-sm text-blue-600 font-bold bg-white rounded-s-lg rounded-s-blue-100 rounded-s-2 border border-white focus:ring-transparent focus:border-blue-300 focus:outline-none"
                    placeholder="Search" required />
            </div>
            <label for="states" class="sr-only">Choose a state</label>
            <select @change="$emit('getPrice')" v-model="currency" id="states"
                class="bg-white w-full border border-white text-gray-900 text-sm rounded-e-lg focus:ring-transparent focus:border-white focus:outline-none block p-3 hover:bg-gray-50">
                <option v-for="(option, index) of options" :value="option" :key="index">{{option}}</option>
            </select>
        </div>
    </div>
</template>
