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

<style scoped lang="scss">
$card-font: sculpin;
$card-bg: white;
.card {
    background-color: $card-bg;
    cursor: grab;
    display: flex;
    flex-direction: column;
    gap: 10px;
    justify-content: space-around;
    margin: 5px;
    padding: 10px;
    border-radius: 4px;
    height: 150px;
    p {
        margin: 0;
        text-align: center;
        font-family: $card-font, sans-serif;
        font-weight: 400;
        font-size: 14px;
        strong {
            font-weight: 700;
        }
        i {
            font-style: italic;
        }
    }
}

</style>
