<script setup>
const model = defineModel()

const props = defineProps({
  id: String,
  labelValue: String,
  name: String
})
</script>

<template>
  <div class="form-item form-item--radiobutton">
    <label :for="id" class="form-item__label form-item__radiobutton-wrapper">
      <input type="radio" v-model="model" :id="id" :name="name" :value="id">
      <span class="custom-radio-checkmark"></span>
      {{ labelValue }}
    </label>
  </div>
</template>

<style lang="scss" scoped>
.form-item__radiobutton-wrapper {
  position: relative;
  padding: 2.8rem 2rem;
  display: flex;
  gap: 0.5rem;
  align-items: center;
  border: 1px solid $secondary-ui-color;
  border-radius: 1rem;
  transition: all 0.2s ease-in;
  cursor: pointer;
}

.form-item__radiobutton-wrapper input{
  width: 0;
  height: 0;
  opacity: 0;
  cursor: pointer;
}

.form-item__radiobutton-wrapper:hover {
  box-shadow: 0 0 2px 0px $primary-ui-color;
}

.form-item__radiobutton-wrapper:has(input:checked) {
  border: 1px solid $primary-ui-color;
  outline: 1px solid $primary-ui-color;
}

.custom-radio-checkmark {
  position: relative;
  background-color: #000;
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  flex-shrink: 0;
  background-color: #fff;
  box-shadow: inset 0px 0px 5px 1px $secondary-ui-color;
  border: 1px solid $secondary-ui-color;
}

.custom-radio-checkmark::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 0.6rem;
  height: 0.6rem;
  background-color: #fff;
  opacity: 0;
  border-radius: 50%;
  transition: opacity 0.2s ease-in;
}

.form-item__radiobutton-wrapper:has(input:checked) .custom-radio-checkmark {
  background-color: $primary-ui-color;
  box-shadow: none;
}

.form-item__radiobutton-wrapper:has(input:checked) .custom-radio-checkmark::after {
  opacity: 1;
}

@media(max-width: $small-screen-size) {
  .form-item__radiobutton-wrapper {
    padding: 1rem;
  }
}
</style>