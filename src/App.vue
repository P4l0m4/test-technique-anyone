<script setup lang="ts">
import { reactive } from 'vue'
import AgeInput from './components/AgeInput.vue'

const student = reactive<{
  name: string
  age: string | null
  image: string | null
}>({
  name: 'Hugh',
  age: null,
  image: 'https://img.fruugo.com/product/0/95/223178950_max.jpg',
})
const handleAgeUpdate = (newAge: string) => {
  student.age = newAge
}
</script>
<template>
  <div class="max-w-lg mx-auto p-4 flex-col gap-16">
    <AgeInput :student="student" @update="handleAgeUpdate" />
  </div>
</template>
