<script setup>
import { ref, reactive } from 'vue';
import ProgressBar from './ui/ProgressBar.vue';
import FormNavigation from './FormNavigation.vue';
import ContactsForm from './form-steps/ContactsForm.vue';
import ServicesForm from './form-steps/ServicesForm.vue';
import BudgetForm from './form-steps/BudgetForm.vue';
import SubmitForm from './form-steps/SubmitForm.vue';

const formData = reactive({
  contacts: {
    name: '',
    email: '',
    phone: '',
    company: ''
  },
  services: ['Development'],
  budget: 's-budget'
})

const formSteps = [
  {
    key: 'contacts',
    step: ContactsForm
  },
  {
    key: 'services',
    step: ServicesForm
  },
  {
    key: 'budget',
    step: BudgetForm
  },
  {
    key: 'submit',
    step: SubmitForm
  }
]

const currentStep = ref(0)
const isFormValid = ref(false)

function handleValidityUpdate(isValid) {
  isFormValid.value = isValid
}

function prevStep() {
  if (currentStep.value > 0) currentStep.value--
}

function nextStep() {
  if (currentStep.value < formSteps.length - 1) currentStep.value++
}

function handleNavigation(action) {
  if (action === 'prev') prevStep()
  if (action === 'next') nextStep()
}
</script>

<template>
  <div class="form-container">
      <ProgressBar
        :total-steps="formSteps.length"
        :current-step="currentStep + 1"
        :is-form-valid="isFormValid"
      />

      <div class="divider"></div>

      <div class="steps-container">
        <component
          v-if="formSteps[currentStep].key !== 'submit'"
          :is="formSteps[currentStep].step"
          v-model="formData[formSteps[currentStep].key]"
          @form-validity-update="handleValidityUpdate"
        ></component>

        <component
          v-else
          :is="formSteps[currentStep].step"
          :form-data="formData"
        ></component>
      </div>
    </div>
    
    <FormNavigation 
      @navigation-action="handleNavigation" 
      :isNextButtonDisabled="!isFormValid"
      :isPrevButtonShown="currentStep > 0"
      :isNextButtonShown="currentStep < formSteps.length - 1"
    />
</template>

<style lang="scss" scoped>
.form-container {
  width: 100%;
  padding: 0rem 3rem 2.25rem;
  box-shadow: 0px 4px 11px 2px $secondary-ui-color;
  border: 1px solid $secondary-ui-color;
  border-radius: 25px;
  min-width: 700px;
}

.divider {
  height: 1px;
  width: 100%;
  background-color: #D9DBE9;
}

.steps-container {
  margin-top: 4rem;
  min-height: 400px;
}

@media(max-width: $large-screen-size) {
  .form-container {
    min-width: unset;
  }
}

@media(max-width: $medium-screen-size) {
  .form-container {
    padding: 0rem 1.5rem 2rem;
  }
  
  .steps-container {
    margin-top: 2rem;
    min-height: unset;
  }
}
</style>