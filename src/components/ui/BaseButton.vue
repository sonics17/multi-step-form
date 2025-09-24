<template>
  <button class="base-button">
    <slot></slot>
  </button>
</template>

<script>
</script>

<style lang="scss" scoped>
.base-button {
  background-color: $primary-ui-color;
  border: 1px solid $primary-ui-color;
  border-radius: 2rem;
  padding: 1.25rem 2.5rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.base-button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.base-button:hover {
  box-shadow: 0px 0px 7px 0px $primary-ui-color;
}

@media(max-width: $small-screen-size) {
  .base-button {
    padding: 1rem 2rem;
  }
}
</style>