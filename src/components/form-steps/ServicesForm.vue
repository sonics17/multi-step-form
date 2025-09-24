<script setup>
import { computed, watch, markRaw } from 'vue';
import Checkbox from '../ui/Checkbox.vue';
import DevelopmentIcon from '@/assets/images/services-icons/development-icon.svg?component'
import WebDesignIcon from '@/assets/images/services-icons/web-design-icon.svg?component'
import MarketingIcon from '@/assets/images/services-icons/marketing-icon.svg?component'
import OtherIcon from '@/assets/images/services-icons/other-icon.svg?component'

const emit = defineEmits(['formValidityUpdate'])

const formDataModel = defineModel()
// model: []

const checkboxes = [
  {
    id: 'development',
    labelValue: 'Development',
    icon: markRaw(DevelopmentIcon)
  },
  {
    id: 'web-design',
    labelValue: 'Web Design',
    icon: markRaw(WebDesignIcon)
  },
  {
    id: 'marketing',
    labelValue: 'Marketing',
    icon: markRaw(MarketingIcon)
  },
  {
    id: 'other',
    labelValue: 'Other',
    icon: markRaw(OtherIcon)
  }
]

const isFormValid = computed(() => {
  return formDataModel.value.length > 0 || false
})

watch(formDataModel, () => {
  emit('formValidityUpdate', isFormValid.value)
}, {immediate: true})
</script>

<template>
  <h2 class="form-title">Our services</h2>
  <p class="paragraph step-description">Please select which service you are interested in.</p>
  <div class="form-items form-items--services">
    <Checkbox 
      v-for="checkbox in checkboxes"
      :key="checkbox.id"
      :id="checkbox.id"
      :label-value="checkbox.labelValue"
      :icon="checkbox.icon"
      v-model="formDataModel"
    />
    <span v-if="!isFormValid" class="error-message">Please select at least one service</span>
  </div>
</template>

<style lang="scss" scoped>
.form-items--services {
  position: relative;
}

.error-message {
  position: absolute;
  bottom: -1.5rem;
  right: 0;
}
</style>