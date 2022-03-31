<template>
  <div>
    <button @click="get">get</button>
    <ul>
      <li v-for="(name, index) in names" :key="index">{{name}}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import {ref} from 'vue';

const headers = {
  Accept: "application/json",
  "Content-Type": "application/json",
};

export default {
  setup() {
    const names = ref(['John','Jane','Joe']);

    async function get() {
      const result = await axios.get("https://jsonplaceholder.typicode.com/posts/1/comments");
      names.value = result.data.map((comment) => comment.name)
    }

    return { names, get };
  },
};
</script>

<style>
button {
  font-size: calc(10px + 2vmin);
  width: 80px;
  margin: 2px;
}
</style>
