<template>
  <UCard>
    <template #header>
      <div class="flex items-center gap-2">
        <UIcon name="i-material-symbols:check-box-outline" />
        Question 1
      </div>
    </template>
    
    <div class="space-y-4">
      <UFormGroup label="Question">
        <UInput placeholder="Enter your question" />
      </UFormGroup>
      <UFormGroup label="Answers">
        <div class="space-y-2">
          <UInput placeholder="Answer A" />
          <UInput placeholder="Answer B" />
          <UInput placeholder="Answer C" />
          <UInput placeholder="Answer D" />
        </div>
      </UFormGroup>
    </div>

    <template #footer>
      Hello
    </template>
  </UCard>
</template>