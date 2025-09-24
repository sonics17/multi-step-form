<script setup>
const props = defineProps({
  id: String,
  labelValue: String,
  icon: Object
})

const model = defineModel()
</script>

<template>
  <div class="form-item form-item--checkbox">
    <input type="checkbox" v-model="model" :id="id" :value="labelValue">
    <label :for="id" class="form-item__label form-item__checkbox-label">
      <div class="form-item__icon-wrapper">
        <component
          :is="icon"
          class="form-item__checkbox-icon"
        ></component>
      </div>
      {{ labelValue }}
    </label>
  </div>
</template>

<style lang="scss" scoped>
.form-item--checkbox input {
  display: none;
}

.form-item__checkbox-label {
  display: flex;
  align-items: center;
  border: 1px solid $secondary-ui-color;
  border-radius: 1rem;
  padding: 1.5rem;
  gap: 0.75rem;
  transition: all 0.2s ease-in;
  cursor: pointer;
}

.form-item__checkbox-label:hover {
  box-shadow: 0 0 2px 0px $primary-ui-color;
}

.form-item--checkbox input:checked + .form-item__checkbox-label{
  border: 1px solid $primary-ui-color;
  outline: 1px solid $primary-ui-color;
}

.form-item__icon-wrapper {
  width: 4.125rem;
  height: 4.125rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #E4E1FF;
}

.form-item__checkbox-icon {
  width: 2.5rem;
  color: $primary-ui-color;
  filter: drop-shadow(0 0 0.15rem rgb(74 58 255 / 0.5));
}

@media(max-width: $small-screen-size) {
  .form-item__checkbox-label {
    padding: 1rem;
  }

  .form-item__icon-wrapper {
    width: 3rem;
    height: 3rem;
  }
  
  .form-item__checkbox-icon {
    width: 2rem;
  }
}
</style>