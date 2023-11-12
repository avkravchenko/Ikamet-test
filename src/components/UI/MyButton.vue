<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.btn {
  background-color: rgb(40, 131, 145);
  border-radius: 5px;
  border: none;
  height: fit-content;
  color: rgb(255, 255, 255);
  padding: 0.5rem 1rem;
  cursor: pointer;

  &:hover {
    background-color: rgb(31, 104, 115);
  }
}
</style>
