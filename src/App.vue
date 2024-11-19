<script setup>
import { ref } from "vue";
import MarkdownEditor from "./components/MarkdownEditor.vue";
// const defaultData = "";
// const comment = ref("");
const textareaId = ref("comment-body2");
// const comment = ref(defaultData)
const items = ref([1,2,3,4,5])
</script>

<template>
  <div class="container">
    <div class="row justify-content-center mt-5">
      <h1>Vue markdown editor</h1>
      <div>
        <!-- <MarkdownEditor :raw-data="comment" :textarea-id="textareaId"/> -->
        <!-- <MarkdownEditor :textarea-id="textareaId"/> -->
        <MarkdownEditor v-for="(item, index) in items" :key="index" :textarea-id="textareaId+index"/>
      </div>
    </div>
    <!-- <button class="btn btn-primary">Primary button</button> -->
  </div>
</template>

<style lang="scss" scoped></style>
