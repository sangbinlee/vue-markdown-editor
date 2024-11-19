<script setup>
import MarkdownIt from "markdown-it";
import { computed, ref } from "vue";

// MarkdownIt, highlight  설정 시작
import hljs from "highlight.js/lib/core";
import css from "highlight.js/lib/languages/css";
import javascript from "highlight.js/lib/languages/javascript";
import json from "highlight.js/lib/languages/json";
import php from "highlight.js/lib/languages/php";
import ruby from "highlight.js/lib/languages/ruby";
import scss from "highlight.js/lib/languages/scss";
import sql from "highlight.js/lib/languages/sql";
import xml from "highlight.js/lib/languages/xml";
import yaml from "highlight.js/lib/languages/yaml";
import "highlight.js/styles/github.css";
import Toolbar from "./Toolbar.vue";

hljs.registerLanguage("javascript", javascript);
hljs.registerLanguage("json", json);
hljs.registerLanguage("yaml", yaml);
hljs.registerLanguage("php", php);
hljs.registerLanguage("ruby", ruby);
hljs.registerLanguage("sql", sql);
hljs.registerLanguage("scss", scss);
hljs.registerLanguage("css", css);
hljs.registerLanguage("xml", xml);

const md = MarkdownIt({
  highlight: (str, lang) => {
    console.log("str", str);
    console.log("lang", lang);
    if (lang && hljs.getLanguage(lang)) {
      try {
        // return (
        //   '<pre><code class="hljs">' +
        //   hljs.highlight(str, { language: lang, ignoreIllegals: true }).value +
        //   "</code></pre>"
        // );
        return `<pre><code class="hljs">
                hljs.highlight(str, {language : lang, ignoreIllegals: true}).value
                </code></pre>`
      } catch (e) {}
    }
    // return '<pre><code class="hljs">'+ md.utils.escapeHtml(str) +'</code></pre>'
    return `<pre><code class="hljs">md.utils.escapeHtml(str)</code></pre>`;
  },
});
// MarkdownIt, highlight  설정 끝

const props = defineProps({
  // rawData: {
  //   type: String,
  //   default: "",
  // },
  textareaId: {
    type: String,
    required: true,
  },
});
// console.log('textareaId=', textareaId)

// const textareaId = ref("comment-body2");

const currentTab = ref("write");
console.log('currentTab.value=', currentTab.value)

const activeTab = computed({
  get: () => currentTab.value,
  set: tab => currentTab.value = tab
  // set: tab => {currentTab.value = tab}
  // set: (tab) => (currentTab.value = tab),
});
console.log('activeTab.value=', activeTab.value)

// 1. currentTab 값을 직접 바꾸는 법
// 2. activeTab 값을 바꿔서 간접적으로 currentTab 값을 바꾸는 법
// 언제 사용하면 좋을까?

// 상하 컴포넌트간 데이터 전달?
// props 는 부모 컴포넌트 -> 자식 컴포넌트 로 데이터를 전달 할때 사용.
// emit 는  자식 컴포넌트 -> 부모 컴포넌트 로 데이터가 아닌 메시지 , 이벤트 를 전달 할때 사용.

// 읽기 전용 계산된 속성 ref 만들기: 
// const preview = computed(() => md.render(props.rawData));
// console.log('preview.value=', preview.value)

// 자식 컴포넌트에서 emit 하여 호출됨
const clear = () => {
  // alert(1)
  console.log('2  자식 컴포넌트에서 emit 하여 호출됨')
  comment.value=''
}

const comment = ref("");
const preview = computed(() => md.render(comment.value));
console.log('preview.value=', preview.value)

</script>

<template>
  <div class="card">
    <div class="card-header">
      <ul class="nav nav-tabs card-header-tabs">
        <li class="nav-item">
          <button
            class="nav-link"
            :class="{ active: currentTab === 'write' }"
            @click="activeTab = 'write'"
          >
            Write
          </button>
        </li>
        <li class="nav-item">
          <button
            class="nav-link"
            :class="{ active: currentTab === 'preview' }"
            @click="activeTab = 'preview'"
          >
            Preview
          </button>
        </li>
      </ul>
    </div>
    <div class="card-body">
      <div class="tab-content">
        <div class="tab-pane" :class="{ active: currentTab === 'write' }">
          <!-- <div class="toolbar" v-if="activeTab === 'write'"> -->
          <div class="toolbar">
            <!-- Vue3 상위컴포넌트로 데이터,이벤트 전달 -->
            <Toolbar :textarea-id="textareaId" @clear-sub="clear"/>
          </div>
          <!-- <slot></slot> -->
          <textarea
            class="form-control"
            rows="10"
            v-model="comment"
            :id="textareaId"
          ></textarea>
        </div>
        <div class="tab-pane preview" :class="{ active: currentTab === 'preview' }">
          <div class="markdown-preview" v-html="preview"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.preview {
  /* min-height: 254px; */
  min-height: 284px;
  background-color: linen;
}
.tab-pane {
  /* height: 284px; */
}

.toolbar {
  /* position: relative; */
  padding-bottom: 5px;
  /* top: 10px;
  right: 16px; */
}
</style>
