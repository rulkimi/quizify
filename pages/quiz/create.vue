<script setup lang="ts">
import type { FormSubmitEvent } from '#ui/types';

const state = reactive({
  title: undefined,
  description: undefined
});

const quizTypes = reactive([
  { label: 'Multiple Choice', icon: 'i-material-symbols:check-box-outline' },
  { label: 'True/False', icon: 'i-material-symbols:check-circle-outline' },
  { label: 'Fill in the Blank', icon: 'i-material-symbols:text-fields' },
  { label: 'Short Answer', icon: 'i-material-symbols:edit-outline' },
  { label: 'Matching', icon: 'i-material-symbols:shuffle' },
  { label: 'Ordering', icon: 'i-material-symbols:arrow-right-alt' },
]);

</script>

<template>
  <UForm :state="state" class="space-y-4">

    <div class="space-y-4">
      <UFormGroup label="Quiz Title" name="quiz-title">
        <UInput v-model="state.title" placeholder="E.g. Fluid Mechanics Topic 1 - Quiz" />
      </UFormGroup>
      <UFormGroup label="Description" name="quiz-description">
        <UTextarea
          v-model="state.description"
          placeholder="E.g. Understand the fundamentals of Fluid Mechanics"
        />
      </UFormGroup>
    </div>

    <div class="bg-white p-0.5 rounded-lg">
      <div class="border border-dashed p-2 rounded-md grid grid-cols-12 gap-1">
        <div 
          v-for="quizType in quizTypes"
          class="bg-white border px-2 py-1 rounded-md col-span-4 hover:bg-gray-100 cursor-pointer flex items-center gap-1"
        >
          <UIcon :name="quizType.icon" class="w-5 h-5" />
          {{ quizType.label }}
        </div>
      </div>
    </div>
  </UForm>
</template>