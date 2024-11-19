<script setup>
import MarkdownIt from 'markdown-it';
import { computed, ref } from 'vue';

import hljs from 'highlight.js/lib/core';
import css from 'highlight.js/lib/languages/css';
import javascript from 'highlight.js/lib/languages/javascript';
import json from 'highlight.js/lib/languages/json';
import php from 'highlight.js/lib/languages/php';
import ruby from 'highlight.js/lib/languages/ruby';
import scss from 'highlight.js/lib/languages/scss';
import sql from 'highlight.js/lib/languages/sql';
import xml from 'highlight.js/lib/languages/xml';
import yaml from 'highlight.js/lib/languages/yaml';
import 'highlight.js/styles/github.css';
import Toolbar from './Toolbar.vue';


hljs.registerLanguage('javascript', javascript)
hljs.registerLanguage('json', json)
hljs.registerLanguage('yaml', yaml)
hljs.registerLanguage('php', php)
hljs.registerLanguage('ruby', ruby)
hljs.registerLanguage('sql', sql)
hljs.registerLanguage('scss', scss)
hljs.registerLanguage('css', css)
hljs.registerLanguage('xml', xml)

const md = MarkdownIt({
  highlight: (str, lang) => {
    console.log('str', str)
    console.log('lang', lang)
    if (lang && hljs.getLanguage(lang)) {
      try {
        return '<pre><code class="hljs">'
                + hljs.highlight(str, {language : lang, ignoreIllegals: true}).value
                + '</code></pre>'
                    
        // return `<pre><code class="hljs">
        //         hljs.highlight(str, {language : lang, ignoreIllegals: true}).value
        //         </code></pre>`

      } catch (e) {
        
      }
    }
    // return '<pre><code class="hljs">'+ md.utils.escapeHtml(str) +'</code></pre>'
    return `<pre><code class="hljs">md.utils.escapeHtml(str)</code></pre>`
  }
})


const props = defineProps({
  rawData:{
    type: String,
    default: ''
  },
  targetId:{
    type: String,
    required:true
  }
})
const currentTab = ref('write')
const preview = computed(()=> md.render(props.rawData))

const activeTab = computed({
  get:() => currentTab.value,
  set: (tab) => currentTab.value = tab
})
</script>

<template>
  <div class="card">
    <div class="card-header">
      <ul class="nav nav-tabs card-header-tabs">
        <li class="nav-item"><button class="nav-link" :class="{ active: activeTab ==='write'}" @click="activeTab = 'write'">Write</button></li>
        <li class="nav-item"><button class="nav-link" :class="{ active: activeTab ==='preview'}" @click="activeTab = 'preview'">Preview</button></li>
      </ul>
      <div class="toolbar" v-if="activeTab ==='write'">
        <Toolbar :target-id="targetId"/>
      </div>
    </div>
    <div class="card-body">
      <div class="tab-content">
        <div class="tab-pane" :class="{ active: activeTab ==='write'}">
          <slot></slot>
        </div>
        <div class="tab-pane" :class="{ active: activeTab ==='preview'}">
          <div class="markdown-preview" v-html="preview"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.markdown-preview{
  min-height: 254px;
}
.toolbar {
  position: absolute;
  top:10px;
  right: 16px;
}
</style>
