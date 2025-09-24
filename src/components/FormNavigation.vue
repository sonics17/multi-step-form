<script setup>
import { nextTick } from 'vue';
import BaseButton from '@/components/ui/BaseButton.vue';

const props = defineProps({
  isNextButtonDisabled: Boolean,
  isPrevButtonShown: Boolean,
  isNextButtonShown: Boolean
})

const emit = defineEmits(['navigation-action'])

function scrollToTop() {
  const formContainer = document.querySelector('.form-container')
  if (formContainer) {
    formContainer.scrollIntoView({
      behavior: 'smooth',
      block: 'start'
    })
  } else {
    window.scrollTo({
      top: 0,
      behavior: 'smooth'
    })
  }
}

async function handlePrev() {
  emit('navigation-action', 'prev')
  await nextTick()
  scrollToTop()
}

async function handleNext() {
  emit('navigation-action', 'next')
  await nextTick()
  scrollToTop()
}
</script>

<template>
  <div class="form-navigation">
    <BaseButton 
      v-if="isPrevButtonShown"
      @click="handlePrev" 
      class="base-button--transparent prev-button"
    >
      Previous step
    </BaseButton>

    <BaseButton 
      v-if="isNextButtonShown"
      @click="handleNext" 
      :disabled="isNextButtonDisabled"
      class="next-button"
    >
      Next step
    </BaseButton>
  </div>
</template>

<style lang="scss" scoped>
.form-navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-top: 2rem;
  gap: 1rem;
  flex-wrap: wrap;
}

.base-button--transparent {
  background-color: transparent;
}

.prev-button {
  margin-right: auto;
}

.next-button {
  margin-left: auto;
}

@media (max-width: $small-screen-size) {
  .form-navigation {
    margin-top: 1rem;
  }
  
  .prev-button, .next-button {
    margin: 0;
    flex: 1 1 auto;
  }
}
</style>