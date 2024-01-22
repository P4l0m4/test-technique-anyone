<script setup lang="ts">
import { computed, ref } from 'vue'

const inputWidth = computed(() => {
  return props.student.age?.length + 'ch'
})

const isInputFocused = ref(false)

function formatInputValue(e: Event) {
  handleInput(e)
  const target = e.target as HTMLInputElement

  props.student.age = target.value
    .replace(/\D/g, '')
    .replace(/\B(?=(\d{3})+(?!\d))/g, ' ')
}

const props = defineProps<{
  student: {
    name: string
    age: string | null
    image: string | null
  }
}>()

const emit = defineEmits(['update:age'])

function handleInput(e: Event) {
  const target = e.target as HTMLInputElement
  emit('update:age', target.value)
}
</script>
<template>
  <div class="flex items-center gap-4">
    <div
      class="bg-gray-300 rounded-full w-20 h-20 image"
      :style="`background-image: url(${props.student.image})`"
      :class="{
        'image--circled': isInputFocused,
      }"
    ></div>
    <div class="flex flex-col gap-2">
      <label
        for="hours-old"
        class="text-base font-normal input-label"
        :class="{
          'input-label--purple': isInputFocused,
        }"
        >{{ props.student.name }} is</label
      >
      <div class="flex gap-3 items-end flex-wrap input-container">
        <input
          v-model="props.student.age"
          name="hours-old"
          @input="formatInputValue"
          @focus="isInputFocused = true"
          @blur="isInputFocused = false"
          id="hours-old"
          class="border-b-gray-300 border-b w-[50px] student-age-input"
          :style="{ width: inputWidth }"
          type="text"
          inputmode="numeric"
        />

        <div class="text text-lg font-normal">hours old</div>
      </div>
    </div>
  </div>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&family=Koulen&display=swap');

.image {
  background-size: cover;
}
.image--circled {
  outline: #4f1edb 2px solid;
  outline-offset: 2px;
}
.input-label {
  font-family: 'Koulen', sans-serif;
}
.input-label--purple {
  color: #4f1edb;
}
.student-age-input {
  min-width: 72px;
  max-width: 220px;
  padding: 0.25rem 0.5rem;
  outline: #d9d5e6 solid 2px;
  border-radius: 4px;
  font-family: 'Inter', sans-serif;
}
.student-age-input:focus {
  outline-color: #4f1edb;
}

.text {
  white-space: nowrap;
  font-family: 'Inter', sans-serif;
}
</style>
