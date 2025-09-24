<script setup>
import MultiStepForm from './components/MultiStepForm.vue';
</script>

<template>
  <div class="outer-wrapper">
    <div class="wrapper">
      <div class="text-content">
        <h1 class="page-title">Get a project quote</h1>
        <p class="paragraph">Please fill the form below to receive a quote for your project. Feel free to add as much detail as needed.</p>
      </div>
      <MultiStepForm />
  </div>
  </div>
</template>

<style lang="scss" scoped>
.outer-wrapper {
  width: 100%;
  padding: 1rem;
}

.wrapper {
  min-height: 100vh;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 44rem;
}

.text-content {
  max-width: 35rem;
  text-align: center;
  margin-bottom: 2.625rem;
}

.page-title {
  margin-bottom: 0.75rem;
}

@media(max-width: $medium-screen-size) {
  .text-content {
    margin-bottom: 1rem;
  }
}
</style>
