<script setup>
import { ref } from 'vue'
import BaseButton from '@/components/ui/BaseButton.vue';
import SubmitImage from '@/assets/images/submit-image.svg?url'

const props = defineProps({
  formData: Object
})

const isSubmitted = ref(false)

function submitFormData() {
  localStorage.setItem('formData', JSON.stringify(props.formData))
  isSubmitted.value = true
}
</script>

<template>
  <div class="form-items form-items--submit">
    <div class="submit-form">
      <img :src="SubmitImage" alt="Submit" class="submit-img">
      <h2 class="form-title">{{ !isSubmitted ? 'Submit your quote request' : 'Request submitted' }}</h2>
      <p class="paragraph step-description">
        <span v-if="!isSubmitted">
          Please review all the information you previously typed in the past steps, and if all is okay, submit your message to receive a project quote in 24 - 48 hours.
        </span>
        <span v-else>
          Thank you! We've received your request and will contact you within 24 - 48 hours.
        </span>
      </p>
      <BaseButton v-if="!isSubmitted" @click="submitFormData">Submit</BaseButton>
    </div>
  </div>
</template>

<style scoped>
.form-items--submit {
  display: grid;
  grid-template-columns: 1fr;
  justify-items: center;
  text-align: center;
}

.submit-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  max-width: 35rem;
  width: 100%;
  min-height: 350px;
}

.submit-img {
  max-width: 9.8rem;
  height: auto;
  margin-bottom: 1.125rem;
}

.step-description {
  max-width: 31.25rem;
  text-align: center;
}
</style>