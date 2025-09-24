<script setup>
import { reactive, watch, computed } from 'vue';
import RadioButton from '../ui/RadioButton.vue';

const emit = defineEmits(['formValidityUpdate'])

const dataFormModel = defineModel()
// model: String

const radioButtons = reactive([
  {
    id: 's-budget',
    labelValue: '$5.000 - $10.000'
  },
  {
    id: 'm-budget',
    labelValue: '$10.000 - $20.000'
  },
  {
    id: 'l-budget',
    labelValue: '$20.000 - $50.000'
  },
  {
    id: 'xl-budget',
    labelValue: '$50.000 +'
  }
])

const isFormValid = computed(() => {
  return dataFormModel.value !== '' || false
})

watch(dataFormModel, () => {
  emit('formValidityUpdate', isFormValid.value)
}, {immediate: true})
</script>

<template>
  <h2 class="form-title">What’s your project budget?</h2>
  <p class="paragraph step-description">Please select the project budget range you have in mind.</p>
  <div class="form-items form-items--budget">
    <RadioButton 
      v-for="radioButton in radioButtons"
      :key="radioButton.id"
      :id="radioButton.id"
      :label-value="radioButton.labelValue"
      :name="'budgetItem'"
      v-model="dataFormModel"
    />
  </div>
</template>

<style scoped>
</style>