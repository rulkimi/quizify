<script setup lang="ts">
const emit = defineEmits(['remove', 'save']);

defineProps<{
  index: number
}>()

const question = ref('');
const type = ref('true-false');
const answers = ref<boolean>(true);
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
      <UFormGroup required label="Question">
        <UInput
          placeholder="Enter your question"
          v-model="question"
        />
      </UFormGroup>

      <UFormGroup required label="Answers">
        <div class="flex gap-4">
          <URadio
            name="correct-answer"
            label="True"
            value="true"
            v-model="answers"
          />
          <URadio
            name="correct-answer"
            label="False"
            value="false"
            v-model="answers"
          />
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
