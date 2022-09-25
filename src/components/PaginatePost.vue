<script setup>
    defineProps(['inicio','fin','limit'])

    const emit=defineEmits(['next','prev'])
    

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button @click="emit('prev')" type="button" class="btn btn-outline-primary" :disabled="inicio<=0">Prev</button>
        <button @click="emit('next')" type="button" class="btn btn-outline-primary" :disabled="fin>=limit">Next</button>
    </div>


</template>
