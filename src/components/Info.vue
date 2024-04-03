<script setup>
import { computed } from 'vue';

const props = defineProps(["image", "currency", "cryptoCurrency", "price"])

const imageUrl = computed(() => {

    return `https://www.cryptocompare.com/${props.image}`;
});

const priceR = computed(() => {
    return parseFloat(props.price.toFixed(2));
});

</script>

<template>
    <div class="flex flex-col items-center justify-center border-t border-blue-300 mx-10 pb-3 px-8">
        <div class="w-10 h-10">
            <img :src="imageUrl" alt="">
        </div>
        <div class="text-gray-500">
            <p>1 <span class="text-gray-600 font-bold">{{ cryptoCurrency }}</span> = {{ priceR }} <span
                    class="text-gray-600 font-bold"> {{ currency }}</span></p>
        </div>
    </div>
</template>
