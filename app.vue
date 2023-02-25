<script setup>
import { ref, reactive, onMounted, watch, Suspense } from "vue";

const test = ref(0);
const text = ref("default text");

const reset = () => (test.value = 0);

const todos = await fetch("https://jsonplaceholder.typicode.com/todos")
  .then((res) => res.json())
  // .then((data) => {
  //   console.log(data);
  //   return data;
  // })
  .catch((error) => console.log(error));

onMounted(() => {
  setInterval(() => test.value++, 1000);
});

watch(text, () => {
  console.log(text.value);
});

console.log(test);
</script>

<template>
  <div>
    <h1 class="text-red-500">{{ test }}</h1>
    <button @click="reset">reset</button>
    <input type="text" v-model="text" />
    <pre>{{ JSON.stringify(todos) }}</pre>
    <Suspense>
      <pre>{{ JSON.stringify(todos) }}</pre>

      <template #fallback> Loading .... </template>
    </Suspense>
    <!-- <NuxtWelcome /> -->
  </div>
</template>
