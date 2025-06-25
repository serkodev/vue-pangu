<script setup lang="ts">
import '@master/normal.css'
import '@master/styles'
import '@master/keyframes.css'

import { onMounted, ref } from 'vue'
import pangu from 'pangu'
import ClipboardJS from 'clipboard'

const copyButton = ref<Element>()
const source = ref('')
const result = ref('')
const blink = ref(false)

const convert = (val: string) => {
  source.value = val
  result.value = pangu.spacing(source.value)
}

const handleTextChanged = (e: Event) => {
  const target = e.target as HTMLInputElement
  convert(target.value)
}

onMounted(() => {
  copyButton.value && new ClipboardJS(copyButton.value)
  convert(source.value)
})
</script>

<template>
  <nav class="h:3.5rem f:gray-10 bg:gray-95">
    <div class="d:flex h:full align-items:center px:24">
      <span class="mr:16 f:16 f:semibold">盤古之白</span>
      <span class="opacity:.4">文案排版轉換 v0.0.2</span>
      <a
        href="https://github.com/serkodev/vue-pangu" target="_blank" class="
      ml:auto
      justify-self:end
      fill:gray_svg
      fill:gray-30_svg:hover
      transition:150ms;ease-in_svg
      "
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
          <path
            d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
          />
        </svg>
      </a>
    </div>
  </nav>

  <div
    class="h:calc(100vh-3.5rem)
    d:grid
    grid-auto-flow:column@xs grid-template-columns:0.5fr;24;0.5fr@xs
    grid-auto-flow:row@<xs grid-template-rows:0.5fr;24;0.5fr@<xs
    px:24 f:fade-16 f:14 pt:8 pb:24
    overflow:auto
    "
  >
    <div class="flex:1">
      <textarea
        class="w:full h:full lh:1.6 overflow:hidden@xs"
        spellcheck="false"
        placeholder="輸入文字 ..."
        :value="source"
        @input="handleTextChanged"
      />
    </div>
    <div class="d:flex">
      <div
        class="
        m:auto
        bl:1;dashed;fade-70@xs h:full@xs w:1@xs
        bt:1;dashed;fade-70@<xs w:full@<xs h:1@<xs
        "
      />
    </div>
    <div
      class="flex:1 opacity:1:hover_.copy rel
    lh:1.6 white-space:pre-wrap word-wrap:anywhere
    overflow:auto@<xs
    "
    >
      <button
        ref="copyButton"
        :data-clipboard-text="result"
        class="
        copy
        fixed
        top:56
        right:24
        abs@<xs
        top:0@<xs
        right:0@<xs
        opacity:1@<xs
        p:6;12
        p:4;8@<xs
        r:6
        bg:fade-76/.9
        bg:fade-70:hover
        bg:green-70!.blink
        opacity:0
        f:gray-30
        f:13
        d:block
        my:8
        opacity:1.blink
        content:'複製'::after
        content:'已複製'.blink::after
        @fade;.5s;calc(2);alternate.blink::after
        "
        :class="{ blink: blink }"
        @click="blink = true"
        @animationend="blink = false"
      />
      <div>{{ result }}</div>
    </div>
  </div>
</template>
