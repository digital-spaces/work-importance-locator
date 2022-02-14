<script setup>
import Card from '@/components/Card.vue'
import onDrop from '@/components/CardSort.vue'

defineProps({
    rank: {
        type: Number,
        required: true
    },
    cards: {
        type: Array,
        required: false
    }
})
</script>

<template>
    <div className='col' :rank=rank @drop="onDrop($event, rank)" @dragover.prevent @dragenter.prevent>
        <Card v-for="item in cards" :id="item.letter" :desc="item.desc" :key="item.letter" :card="item" />
    </div>
</template>