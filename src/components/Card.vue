<script setup>
import { onMounted, ref } from 'vue';
import Arrows from './icons/Arrows.vue';
import axios from 'axios';
import SelectInputForm from './SelectInputForm.vue';
import Info from './Info.vue';

var currencyAmount = ref(1);
var currency = ref("USD");
var cryptoAmount = ref("0.00");
var cryptoCurrency = ref("BTC");
var price = ref(0);
var image = ref("");

const currencies = ["USD", "EUR", "BS"];
const cryptoCurrencies = ["BTC", "ETH", "SOL", "DOGE", "BNB", "USDT"];

async function getPrice() {
    const { data } = await axios.get(`https://min-api.cryptocompare.com/data/pricemultifull?fsyms=${encodeURI(cryptoCurrency.value)}&tsyms=${encodeURI(currency.value)}`);

    const { RAW } = data;
    const dataCrypto = RAW[cryptoCurrency.value];
    const info = dataCrypto[currency.value];

    price.value = info.PRICE;
    image.value = info.IMAGEURL;

    cryptoAmount.value = parseFloat((currencyAmount.value / price.value).toFixed(8));

}

onMounted(() => {
    getPrice();
});

</script>
<template>
    <div class="flex flex-col min-w-fit border rounded-lg shadow bg-blue-50 border-blue-300">

        <div class="flex flex-row min-w-full">
            <SelectInputForm v-model:currencyAmount="currencyAmount" v-model:currency="currency" :label="'From: '"
                :options="currencies" @get-price="getPrice" />
            <div class="flex flex-col justify-center relative leading-normal py-6 ">
                <Arrows
                    class="w-8 h-8 mt-5 border border-blue-300 flex items-center justify-center bg-blue-50 rounded-full shadow-md" />
            </div>
            <SelectInputForm v-model:currencyAmount="cryptoAmount" v-model:currency="cryptoCurrency" :label="'To: '"
                :options="cryptoCurrencies" @get-price="getPrice" />

        </div>
        <Info :image="image" :currency="currency" :crypto-currency="cryptoCurrency" :price="price" />
    </div>
</template>
