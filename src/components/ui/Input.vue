<script setup>
import { ref, onMounted } from 'vue'
import { vMaska } from 'maska/vue'

const props = defineProps({
  id: String,
  labelValue: String,
  type: String,
  placeholder: String,
  icon: Object
})

const model = defineModel()
const errorMessage = ref('')
const isValid = ref(false)

const emit = defineEmits(['inputValidation'])

function onlyDigits(value) {
  return (value || '').replace(/\D/g, '')
}

function validateInput(showError = true) {
  errorMessage.value = ''
  let valid = true

  if (!model.value || !model.value.trim()) {
    if (showError) errorMessage.value = 'This field is required'
    valid = false
    isValid.value = valid
    return valid
  }

  switch (props.type) {
    case 'text':
      let value = model.value.trim()
      value = value.replace(/[0-9]/g, '')
      if (props.id === 'name' && value.length < 2) {
        if (showError) errorMessage.value = 'This field requires at least 2 characters'
        valid = false
      }
      break

    case 'email':
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      if (!emailRegex.test(model.value)) {
        if (showError) errorMessage.value = 'Enter correct email'
        valid = false
      }
      break

    case 'tel':
      const cleanPhone = onlyDigits(model.value)
      if (cleanPhone.length !== 10) {
        if (showError) errorMessage.value = 'Enter correct phone number (10 digits)'
        valid = false
      }
      break
  }

  isValid.value = valid
  return valid
}

function handleBlur() {
  if (model.value) {
    let value = model.value.trim()

    if (props.id === 'name') {
      value = value.replace(/[0-9]/g, '')
    }
    
    value = value.replace(/\s+/g, ' ')
    model.value = value
  }
  
  validateInput(true)
  emit('inputValidation', { id: props.id, isValid: isValid.value })
}

function handleInput() {
  const valid = validateInput(false)
  emit('inputValidation', { id: props.id, isValid: valid })
}

onMounted(() => {
  handleInput()
})
</script>

<template>
  <div class="form-item form-item--input">
    <label :for="id" class="form-item__label"> {{ labelValue }} </label>
    <div class="form-item__input-container">
      <component
        :is="icon"
        class="form-item__input-icon"
      ></component>
      <input
        v-model="model"
        v-maska="type === 'tel' ? '(###) ###-####' : null"
        :id="id"
        :type="type"
        :placeholder="placeholder"
        :autocomplete="id === 'email' ? 'email' : id === 'name' ? 'name' : 'on'"
        :name="id"
        @blur="handleBlur"
        @input="handleInput()"
        class="form-item__input"
      />
    </div>
    <span v-if="errorMessage" class="error-message">{{ errorMessage }}</span>
  </div>
</template>


<style lang="scss" scoped>
.form-item--input {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 1.125rem;
}

.form-item--input input {
  padding: 1.25rem 3rem 1.25rem 1.25rem;
  border: 1px solid $secondary-ui-color;
  box-shadow: 0px 2px 5px 0px $secondary-ui-color;
  border-radius: 2rem;
  transition: all 0.2s ease-in;
  width: 100%;
}

.form-item--input input:focus {
  outline: none;
  border: 1px solid $primary-ui-color;
  box-shadow: none;
}

.form-item__input-container {
  position: relative;
  display: flex;
  align-items: center;
}

.form-item__input-icon {
  position: absolute;
  max-width: 1.5rem;
  max-height: 1.75rem;
  width: auto;
  height: auto;
  right: 1.25rem;
  top: 50%;
  transform: translateY(-50%);
  flex-shrink: 0;
  color: $icon-ui-color;
  transition: all 0.2s ease-in;
}

.form-item__input-container:focus-within .form-item__input-icon {
  color: $primary-ui-color;
}

.error-message {
  position: absolute;
  display: flex;
  align-items: center;
  min-height: 1.5rem;
  bottom: -1.6rem;
}

@media(max-width: $medium-screen-size) {
  .form-item--input {
    gap: 0.75rem;
  }
}

@media(max-width: $small-screen-size) {
  .form-item--input {
    margin-bottom: 1rem;
  }

  .form-item--input input {
    padding: 0.8rem 3rem 0.8rem 1.25rem;
  }
  
  .error-message {
    bottom: -1.8rem;
  }
}
</style>
