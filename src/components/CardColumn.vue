<script setup>
import onDrop from '@/views/CardSortView.vue'

defineProps({
    rank: {
        type: Number,
        required: true
    },
    list: {
        type: Array,
        required: true
    },
    onDrop: {
        type: Function,
        required: true
    }
})
</script>

<template>
        <div 
            className='col'
            :rank=rank
            @drop="onDrop($event, 4)"
            @dragover.prevent 
            @dragenter.prevent
            :valid="list.length==4 ? 'yes' : 'no'"
        >
            <h2>Rank {{rank}}</h2>
            <h3>{{list.length}} / 4</h3>
            <slot/>
        </div>
</template>