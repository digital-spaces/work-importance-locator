<script setup>
defineProps({
    letter: {
        type: String,
        required: true
    },
    desc: {
        type: String,
        required: true
    }
})
</script>

<template>
    <div className='card' id={{letter}} >
        <p><i>On my <strong>ideal</strong> job, it is important that...</i></p>
        <p><strong>...{{desc}}</strong></p>
    </div>
</template>

<style scoped>
.card {
    background-color: white;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 10px;
    margin: 5px;
    gap: 10px;
}

.card p {
    text-align: center;
    margin: 0;
}
</style>
