<script setup>
import { ref, nextTick, onMounted } from 'vue';

const props = defineProps({
  totalSteps: Number,
  currentStep: Number
})

const isFirstAnimation = ref(true)

function getStepClass(step) {
  if (step < props.currentStep) {
    return 'step--completed'
  } else if (step === props.currentStep) {
    return isFirstAnimation.value ? '' :'step--current'
  } else {
    return ''
  }
}

function getConnectorClass(step) {
  if (step < props.currentStep) {
    return 'connector--completed'
  } else if (step === props.currentStep) {
    return isFirstAnimation.value ? '' : 'connector--current'
  } else {
    return ''
  }
}

onMounted(async () => {
  await nextTick()
  setTimeout(() => { 
    isFirstAnimation.value = false 
  }, 5)
})
</script>

<template>
  <div class="progress-bar">
    <div 
      v-for="step in totalSteps"
      :key="step"
      class="step-wrapper"
    >
      <div 
        class="step-circle progress-step"
        :class="getStepClass(step)"
      >
        {{ step }}
      </div>
      <div
        v-if="step !== totalSteps"
        class="step-connector"
        :class="getConnectorClass(step)"
      ></div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.progress-bar {
  display: flex;
  justify-content: space-between;
  gap: 1.125rem;
  padding: 2rem 1.3rem;
}

.step-wrapper {
  display: flex;
  align-items: center;
  flex: 1 1 auto;
  gap: 1.125rem;
}

.step-wrapper:last-child {
  flex: 0 0 auto;
}

.step-circle {
  width: 2.125rem;
  height: 2.125rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: $secondary-ui-color;
  color: $secondary-text-color;
  flex: 0 0 auto;
  transition: all .3s ease-in;
  transition-delay: 0.2s;
}

.step--current, .step--completed {
  background-color: $primary-ui-color;
  color: #fff;
}

.step-connector {
  position: relative;
  height: 0.375rem;
  flex: 1 1 auto;
  background-color: $secondary-ui-color;
  border-radius: 0.5rem;
}

.step-connector::after {
  content: '';
  position: absolute;
  width: 0%;
  height: 100%;
  border-radius: inherit;
  background-color: $primary-ui-color;
  transition: width 0.3s ease;
}

.connector--current::after {
  width: 50%;
  transition: width 0.5s ease;
  transition-delay: 0.3s;
}

.step-connector::after, .connector--current::after:last-child, .step-circle {
  transition-delay: 0s;
}

.connector--completed::after {
  transition: width 0.3s ease;
  width: 100%;
}

.step-circle:last-child {
  transition-delay: 0s;
}

@media(max-width: $medium-screen-size) {
  .progress-bar {
    padding: 2rem 0rem;
    gap: 0rem;
  }

  .step-wrapper {
    gap: 0rem;
  }

  .step-connector {
    box-sizing: content-box;
    margin: 0 -4px;
    z-index: -100;
  }
}

@media(max-width: $medium-screen-size) {
  .progress-bar {
    padding: 1rem 0rem;
  }
}
</style>