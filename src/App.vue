<script setup>
import Card from './components/Card.vue';
import ReloadPrompt from './components/ReloadPrompt.vue';

</script>

<template>
  <header>
    <div class="wrapper">
    </div>
  </header>

  <main>
        <div class="py-10 flex flex-col justify-center items-center">
            <h1 class="text-2xl mb-2 font-semibold">Crypto Currency Exchanger</h1>
            <Card/>
        </div>
  </main>
    <ReloadPrompt />
</template>
