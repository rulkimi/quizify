<script setup lang="ts">
const emit = defineEmits(['remove', 'save']);

const props = defineProps<{
  index: number
  quizMode: 'edit' | 'answer'
}>()

const mode = ref(props.quizMode)
const question = ref('');
const type = ref('true-false');
const answers = ref<boolean>(true); // Make sure answers is a boolean
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
        <div class="flex gap-4">
          <template v-if="mode === 'edit'">
            <URadio
              :name="'correct-answer-' + index"
              label="True"
              :value="true"
              v-model="answers"
            />
            <URadio
              :name="'correct-answer-' + index"
              label="False"
              :value="false"
              v-model="answers"
            />
          </template>
          <span v-if="mode === 'answer'">
            {{ answers ? 'True' : 'False' }}
          </span>
        </div>
      </UFormGroup>
    </div>

    <template #footer>
      <div class="flex justify-end items-center gap-2">
        <UButton variant="link" @click="emit('remove')">Remove</UButton>
        <UButton v-if="mode === 'edit'" @click="mode = 'answer'; emit('save', { type, question, answers })">Save</UButton>
        <UButton v-else @click="mode = 'edit'">Edit</UButton>
      </div>
    </template>

  </UCard>
</template>
