<template>
  <h1>BELAJAR PINIA</h1>
  <p>Akses count: {{ countStore.count }}</p>
  <p>Akses double count: {{ countStore.doubleCount }}</p>
  <button class="counter" @click="countStore.increment">+</button><br /><br />
  <button class="counter" @click="countStore.decrement">-</button><br /><br />
</template>

<script>
import { useCountStore } from '../store/countStore';

export default {
  setup() {
    const countStore = useCountStore();
    return { countStore };

  },
};
</script>

