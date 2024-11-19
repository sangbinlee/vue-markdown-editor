<script setup lang="ts">
import "@github/markdown-toolbar-element";
// @import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css");
defineProps({
  textareaId: {
    type: String,
    required: true,
  },
});

//Vue3 상위컴포넌트로 데이터,이벤트 전달
const emit = defineEmits(['clearSub']);


// const comment = ref("");
// const clear = () => {
//   // alert(1)
//   console.log('1 clear textarea')
//   // emit('clear')
// }

</script>
<template>
  <markdown-toolbar :for="textareaId" class="gap-5">
    <md-bold class="btn btn-sm btn-light">
      <i class="bi bi-type-bold"></i>
    </md-bold>
    <md-header class="btn btn-sm btn-light">
      <i class="bi bi-type-h3"></i>
    </md-header>
    <md-italic class="btn btn-sm btn-light">
      <i class="bi bi-type-italic"></i>
    </md-italic>
    <md-quote class="btn btn-sm btn-light">
      <i class="bi bi-quote"></i>
    </md-quote>
    <md-code class="btn btn-sm btn-light">
      <i class="bi bi-code"></i>
    </md-code>
    <md-link class="btn btn-sm btn-light">
      <i class="bi bi-link-45deg"></i>
    </md-link>
    <md-image class="btn btn-sm btn-light">
      <i class="bi bi-image"></i>
    </md-image>
    <md-unordered-list class="btn btn-sm btn-light">
      <i class="bi bi-list-ul"></i>
    </md-unordered-list>
    <md-ordered-list class="btn btn-sm btn-light">
      <i class="bi bi-list-ol"></i>
    </md-ordered-list>
    <md-task-list class="btn btn-sm btn-light">
      <i class="bi bi-list-task"></i>
    </md-task-list>
    <md-mention class="btn btn-sm btn-light">
      <i class="bi bi-at"></i>
    </md-mention>
    <md-ref class="btn btn-sm btn-light">
      <i class="bi bi-type-h1"></i>
    </md-ref>
    <button data-md-button class="btn btn-sm btn-light clear" 
    @click="$emit('clearSub')"
    >clear</button>
    <!-- @click="clear" -->
  </markdown-toolbar>
  <!-- <textarea id="textarea_id"></textarea> -->
   
  <!-- <textarea
            class="form-control"
            rows="10"
            v-model="comment"
            id="comment-body"
          ></textarea> -->
</template>

<style scoped>

.clear{
  /* right: 0 !important;
  position: absolute !important; */
  float: right
}
</style>
