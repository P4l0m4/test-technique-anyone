<script setup lang="ts">
import { computed } from 'vue'

const inputWidth = computed(() => {
  return props.student.age?.length + 'ch'
})

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
  <div class="flex items-center gap-2">
    <div
      class="bg-gray-300 rounded-full w-14 h-14 image"
      :style="`background-image: url(${props.student.image})`"
    ></div>
    <div class="flex-col">
      <label for="hours-old">{{ props.student.name }} is</label>
      <div class="flex gap-2 items-end flex-wrap">
        <input
          v-model="props.student.age"
          name="hours-old"
          @input="formatInputValue"
          id="hours-old"
          class="border-b-gray-300 border-b w-[50px] student-age-input"
          :style="{ width: inputWidth }"
          type="text"
          inputmode="numeric"
        />

        <div class="text">hours old</div>
      </div>
    </div>
  </div>
</template>
<style>
.image {
  background-size: cover;
}
.student-age-input {
  min-width: 72px;
  max-width: 220px;
  padding: 0.25rem 0.5rem;
}
.text {
  white-space: nowrap;
}
</style>
