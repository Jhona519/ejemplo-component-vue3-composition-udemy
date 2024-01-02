<script setup>

defineProps(["inicio" , "fin" , "maxlength"]);

const emit = defineEmits(["next","prev"])

</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic example">
  <button @click="emit('prev')" type="button" class="btn btn-outline-primary" :disabled="inicio === 0" >Previus</button>
  <button @click="emit('next')" type="button" class="btn btn-outline-primary" :disabled="fin >= maxlength">Next</button>
</div>
</template>
<style></style>