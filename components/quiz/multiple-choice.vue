<script setup lang="ts">
const emit = defineEmits(['remove', 'save']);

const question = ref('');
const type = ref('multiple-choice')
const answers = ref([
  { text: '', correct: false },
  { text: '', correct: false },
  { text: '', correct: false },
  { text: '', correct: false },
]);

const setCorrectAnswer = (index: number) => {
  answers.value.forEach((answer, i) => {
    answer.correct = i === index;
  });
};
</script>

<template>
  <UCard>
    <template #header>
      <div class="flex items-center gap-2">
        <UIcon name="i-material-symbols:check-box-outline" />
        Question 1
      </div>
    </template>

    <div class="space-y-4">
      <UFormGroup required label="Question">
        <UInput
          placeholder="Enter your question"
          v-model="question"
        />
      </UFormGroup>

      <UFormGroup required label="Answers">
        <div class="space-y-2">
          <div
            v-for="(answer, index) in answers"
            :key="index"
            class="flex items-center gap-2"
          >
            <UInput
              class="flex-grow"
              :placeholder="`Answer ${String.fromCharCode(65 + index)}`"
              v-model="answer.text"
            />
            <URadio
              name="correct-answer"
              :value="index"
              :checked="answer.correct"
              @change="setCorrectAnswer(index)"
            />
          </div>
        </div>
      </UFormGroup>
    </div>

    <template #footer>
      <div class="flex justify-end items-center gap-2">
        <UButton variant="link" @click="emit('remove')">Remove</UButton>
        <UButton @click="emit('save', { type, question, answers })">Save</UButton>
      </div>
    </template>

  </UCard>
</template>
