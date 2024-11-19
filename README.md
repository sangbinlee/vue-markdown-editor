# vue-markdown-editor

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

###  따라하기 youtube 
### https://www.youtube.com/watch?v=syjJ8DXnjzY
```
Vue 3 project - Build a GitHub-like Markdown Editor with Syntax highlights supports
```

### 소스 설명
#### 1. dependencies
```
  "dependencies": {
    "@github/markdown-toolbar-element": "^2.2.3",
    "highlight.js": "^11.10.0",
    "markdown-it": "^14.1.0",
    "vue": "^3.5.12"
  },
```

#### 2. bootstrap@5.3.3
#####  index.html   
```
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" >

```

#### 3. 설정
#####  vite.config.js
```
const customElements = [
  'markdown-toolbar',
  'md-bold',
  'md-header',
  'md-italic',
  'md-quote',
  'md-code',
  'md-link',
  'md-image',
  'md-unordered-list',
  'md-ordered-list',
  'md-task-list',
  'md-mention',
  'md-ref',
]

// https://vite.dev/config/
export default defineConfig({
  plugins: [
    vue({
      template:{
        compilerOptions:{
          isCustomElement: (tag) => customElements.includes(tag)
        }
      }

```



#### 4. 소스
#####  src\App.vue
#####  컴포넌트 MarkdownEditor 사용
#####  컴포넌트 MarkdownEditor 의 slot 영역 사용
```
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
```
#####  설명
```

```"# vue-markdown-editor" 
