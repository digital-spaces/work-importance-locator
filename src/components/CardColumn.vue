<script setup>
import onDrop from '@/components/CardSort.vue'

defineProps({
    rank: {
        type: Number,
        required: true
    },
    list: {
        type: Array,
        required: true
    }
})
</script>

<template>
        <div 
            className='col'
            :rank=rank
            @drop="onDrop($event, rank)" 
            @dragover.prevent 
            @dragenter.prevent
            :valid="list.length==4 ? 'yes' : 'no'"
        >
            <h2>Rank {{rank}}</h2>
            <h3>{{list.length}} / 4</h3>
            <slot/>
        </div>
</template>