<script setup>
import { computed, reactive, markRaw } from 'vue';
import Input from '../ui/Input.vue';
import NameIcon from '@/assets/images/contacts-icons/name-icon.svg?component'
import EmailIcon from '@/assets/images/contacts-icons/email-icon.svg?component'
import PhoneIcon from '@/assets/images/contacts-icons/phone-icon.svg?component'
import CompanyIcon from '@/assets/images/contacts-icons/company-icon.svg?component'

const emit = defineEmits(['formValidityUpdate'])

const formDataModel = defineModel()
// model: {
//   name: '',
//   email: '',
//   phone: '',
//   company: ''
// }

const inputFields = reactive([
  {
    id: 'name',
    labelValue: 'Name',
    type: 'text',
    placeholder: 'John Carter',
    icon: markRaw(NameIcon)
  },
  {
    id: 'email',
    labelValue: 'Email',
    type: 'email',
    placeholder: 'Email address',
    icon: markRaw(EmailIcon)
  },
  {
    id: 'phone',
    labelValue: 'Phone Number',
    type: 'tel',
    placeholder: '(123) 456 - 7890',
    icon: markRaw(PhoneIcon)
  },
  {
    id: 'company',
    labelValue: 'Company',
    type: 'text',
    placeholder: 'Company name',
    icon: markRaw(CompanyIcon)
  }
])

const validationMap = reactive(new Map())

const isFormValid = computed(() => {
  const values = [...validationMap.values()]
  return values.every(value => value === true)
})

function handleFieldValidation({id, isValid}) {
  validationMap.set(id, isValid)
  emit('formValidityUpdate', isFormValid.value)
}
</script>

<template>
  <h2 class="form-title">Contact details</h2>
  <p class="paragraph step-description">Lorem ipsum dolor sit amet consectetur adipisc.</p>
  <div class="form-items form-items--contacts">
    <Input
      v-for="field in inputFields"
      :key="field.id"
      v-model="formDataModel[field.id]"
      :id="field.id"
      :label-value="field.labelValue"
      :type="field.type"
      :placeholder="field.placeholder"
      :icon="field.icon"
      @input-validation="handleFieldValidation"
    />
  </div>
</template>

<style scoped>
</style>