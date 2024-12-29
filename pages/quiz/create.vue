<script setup lang="ts">
import { reactive, ref, markRaw } from 'vue';
import QuizMultipleChoice from '../../components/quiz/multiple-choice.vue';
import QuizTrueFalse from '../../components/quiz/true-false.vue';
import QuizFillInTheBlank from '../../components/quiz/fill-in-the-blank.vue';
import QuizShortAnswer from '../../components/quiz/short-answer.vue';
import QuizMatching from '../../components/quiz/matching.vue';
import QuizOrdering from '../../components/quiz/ordering.vue';
import type { FormSubmitEvent } from '#ui/types';

const state = reactive({
  title: '',
  description: '',
});

interface Quiz {
  label: string;
  icon: string;
  component: any;
}

const quizTypes = reactive<Quiz[]>([
  { label: 'Multiple Choice', icon: 'i-material-symbols:check-box-outline', component: markRaw(QuizMultipleChoice) },
  { label: 'True/False', icon: 'i-material-symbols:check-circle-outline', component: markRaw(QuizTrueFalse) },
  { label: 'Fill in the Blank', icon: 'i-material-symbols:text-fields', component: markRaw(QuizFillInTheBlank) },
  { label: 'Short Answer', icon: 'i-material-symbols:edit-outline', component: markRaw(QuizShortAnswer) },
  { label: 'Matching', icon: 'i-material-symbols:shuffle', component: markRaw(QuizMatching) },
  { label: 'Ordering', icon: 'i-material-symbols:arrow-right-alt', component: markRaw(QuizOrdering) },
]);

const questions = ref<Quiz[]>([]);

function addQuestion(quizType: Quiz) {
  questions.value.push(quizType);
}

function removeQuestion(index: number) {
  questions.value.splice(index, 1);
}

interface QuizQuestion {
  question: string;
  type: 'multiple-choice' | 'true-false' | 'fill-in-the-blank' | 'short-answer' | 'matching' | 'ordering';
  answers: 
    | { text: string; correct: boolean }[]
    | boolean
    | { text: string }[]                  
    | { left: string; right: string }[]  
    | { text: string; order: number }[];
}

const saveQuizQuestion = (quiz: QuizQuestion) => {
  console.log(quiz.answers)
}
</script>

<template>
  <UForm :state="state" class="space-y-4 w-1/2">
    <UCard>
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
    </UCard>

    <div class="bg-white p-0.5 rounded-lg">
      <div class="border border-dashed p-2 rounded-md grid grid-cols-12 gap-1">
        <div
          v-for="quizType in quizTypes"
          :key="quizType.label"
          class="bg-white border px-2 py-1 rounded-md col-span-4 hover:bg-gray-100 cursor-pointer flex items-center gap-1"
          @click="addQuestion(quizType)"
        >
          <UIcon :name="quizType.icon" class="w-5 h-5" />
          {{ quizType.label }}
        </div>
      </div>
    </div>

    <div v-if="questions.length > 0" class="space-y-4">
      <div 
        v-for="(question, index) in questions" 
        :key="index"
        class="relative bg-gray-100 p-2 rounded-lg"
      >
        <component
          :is="question.component"
          :index="index + 1"
          quiz-mode="edit"
          @remove="removeQuestion(index)"
          @save="saveQuizQuestion"
        />
      </div>
    </div>
  </UForm>
</template>
