<script setup>
import { ref } from "vue";
import MarkdownEditor from "./components/MarkdownEditor.vue";

const defaultData = "";

/*
```javascript
console.log('testing')
*/

const comment = ref("");
// const comment = ref(defaultData)
</script>

<template>
  <div class="container">
    <div class="row justify-content-center mt-5">
      <h1>Vue markdown editor</h1>
      <div>
        <MarkdownEditor :raw-data="comment" target-id="comment-body">
          <textarea
            class="form-control"
            rows="10"
            v-model="comment"
            id="comment-body"
          ></textarea>
        </MarkdownEditor>
      </div>
    </div>
    <!-- <button class="btn btn-primary">Primary button</button> -->
  </div>
</template>

<style lang="scss" scoped></style>
