<script setup lang="ts">
const emit = defineEmits(['remove', 'save', 'answer']);

const props = defineProps<{
  index: number,
  quizMode: 'edit' | 'answer'
}>()

const mode = ref(props.quizMode);
const question = ref('');
const type = ref('multiple-choice');
const answers = ref([
  { text: '', correct: true },
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
        Question {{ index }}
      </div>
    </template>

    <div class="space-y-4">
      <UFormGroup
        :required="mode === 'edit'"
        label="Question"
      >
        <div class="text-lg font-semibold" v-if="mode === 'answer'">{{ question }}</div>
        <UInput
          v-if="mode === 'edit'"
          placeholder="Enter your question"
          v-model="question"
        />
      </UFormGroup>

      <UFormGroup 
        :required="mode === 'edit'"
        label="Answers"
      >
        <div class="space-y-2">
          <div
            v-for="(answer, idx) in answers"
            :key="idx"
            class="flex items-center gap-2"
          >
            <div class="flex-grow">
              <div v-if="mode === 'answer'">
                <span :class="{'font-bold text-green-600': answer.correct}">
                  {{ String.fromCharCode(65 + idx) }}) {{ answer.text }}
                </span>
              </div>
              <UInput
                v-if="mode === 'edit'"
                :id="`answer-choice-${index}-${idx}`"
                class="flex-grow"
                :placeholder="`Answer ${String.fromCharCode(65 + idx)} ${answer.correct ? '- Correct Answer' : '' }`"
                v-model="answer.text"
              />
            </div>
            <div v-if="mode === 'answer'">
              <span v-if="answer.correct" class="text-green-500">
                Correct
              </span>
            </div>
            <URadio
              v-if="mode === 'edit'"
              :name="'correct-answer-' + index"
              :value="idx"
              :checked="answer.correct"
              @change="setCorrectAnswer(idx)"
            />
          </div>
        </div>
      </UFormGroup>
    </div>

    <template #footer>
      <div class="flex justify-end items-center gap-2">
        <UButton variant="link" @click="emit('remove')">Remove</UButton>
        <UButton v-if="mode === 'edit'" @click="mode = 'answer'; emit('save', { index, type, question, answers })">Save</UButton>
        <UButton v-else @click="mode = 'edit'">Edit</UButton>
      </div>
    </template>
  </UCard>
</template>

