<script setup>
defineProps({
    rank: {
        type: Number,
        required: true
    }
})
</script>

<template>
    <div className='col' rank={{rank}}></div>
</template>