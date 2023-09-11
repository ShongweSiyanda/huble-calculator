<template>
  <button class="btn btn-maths px-lg-4 px-3 py-lg-3 py-2 text-center fw-bold me-2" @click="handleClick">
    {{ operator }}
  </button>
</template>
<script setup>
const props = defineProps({
  operator: String
})
const emits = defineEmits(['click'])

const handleClick = () => {
  emits('click')
}

</script>
<style scoped>
.btn-maths {
  background-color: #003562;
  color: #fff;
  opacity: 1;
  transition: all .3s ease-in-out;
}

.btn-maths:hover {
  background-color: #003562;
  opacity: 0.8;
}
</style>