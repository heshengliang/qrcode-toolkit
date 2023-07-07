<script setup lang="ts">
import type { MarginObject } from '~/logic/types'
import { resolveMargin } from '~/logic/utils'

const margin = defineModel<number | MarginObject>('modelValue', {
  type: [Object, Number],
  required: true,
})

const left = computed({
  get: () => {
    if (typeof margin.value === 'number')
      return margin.value

    return margin.value.left
  },
  set: (value) => {
    if (typeof margin.value === 'number') {
      margin.value = value
      return
    }
    margin.value.left = value
  },
})

const right = computed({
  get: () => {
    if (typeof margin.value === 'number')
      return margin.value

    return margin.value.right
  },
  set: (value) => {
    if (typeof margin.value === 'number') {
      margin.value = value
      return
    }
    margin.value.right = value
  },
})

const top = computed({
  get: () => {
    if (typeof margin.value === 'number')
      return margin.value

    return margin.value.top
  },
  set: (value) => {
    if (typeof margin.value === 'number') {
      margin.value = value
      return
    }
    margin.value.top = value
  },
})

const bottom = computed({
  get: () => {
    if (typeof margin.value === 'number')
      return margin.value

    return margin.value.bottom
  },
  set: (value) => {
    if (typeof margin.value === 'number') {
      margin.value = value
      return
    }
    margin.value.bottom = value
  },
})
</script>

<template>
  <template v-if="(typeof margin === 'number')">
    <OptionItem title="Margin">
      <OptionSlider v-model="margin" :min="0" :max="20" :step="1" />
      <button
        icon-button-sm
        @click="margin = resolveMargin(margin)"
      >
        <div i-ri-arrow-down-s-line />
      </button>
    </OptionItem>
  </template>
  <template v-else>
    <OptionItem title="Margin">
      <div flex-auto />
      <button
        icon-button-sm
        @click="margin = margin.top"
      >
        <div i-ri-arrow-up-s-line />
      </button>
    </OptionItem>
    <OptionItem title="left" nested>
      <OptionSlider v-model="left" :min="0" :max="20" :step="1" />
    </OptionItem>
    <OptionItem title="right" nested>
      <OptionSlider v-model="right" :min="0" :max="20" :step="1" />
    </OptionItem>
    <OptionItem title="top" nested>
      <OptionSlider v-model="top" :min="0" :max="20" :step="1" />
    </OptionItem>
    <OptionItem title="bottom" nested>
      <OptionSlider v-model="bottom" :min="0" :max="20" :step="1" />
    </OptionItem>

    <!-- <OptionItem title="Top" nested>
      <OptionSlider v-model="margin.top" :min="0" :max="20" :step="1" />
    </OptionItem>
    <OptionItem title="Bottom" nested>
      <OptionSlider v-model="margin.bottom" :min="0" :max="20" :step="1" />
    </OptionItem>
    <OptionItem title="Left" nested>
      <OptionSlider v-model="margin.left" :min="0" :max="20" :step="1" />
    </OptionItem>
    <OptionItem title="Right" nested>
      <OptionSlider v-model="margin.right" :min="0" :max="20" :step="1" />
    </OptionItem> -->
  </template>
</template>
