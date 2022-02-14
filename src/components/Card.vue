<script setup>
function startDrag(e, item) {
    e.dataTransfer.dropEffect = 'move';
    e.dataTransfer.effectAllowed = 'move';
    e.dataTransfer.setData('itemID', item.letter);
    console.log();
}

defineProps({
    id: {
        type: String,
        required: true
    },
    desc: {
        type: String,
        required: true
    },
    card: {
        type: Object,
        required: true
    }
})
</script>

<template>
    <div 
      className="card"
      :id="id" 
      draggable=true 
      @dragstart="startDrag($event, card)"
    >
        <p><i>On my <strong>ideal</strong> job, it is important that...</i></p>
        <p><strong>...{{desc}}</strong></p>
    </div>
</template>

<style scoped>
.card {
    background-color: white;
    cursor: grab;
    display: flex;
    flex-direction: column;
    gap: 10px;
    justify-content: space-around;
    margin: 5px;
    padding: 10px;
}

.card p {
    margin: 0;
    text-align: center;
}
</style>
