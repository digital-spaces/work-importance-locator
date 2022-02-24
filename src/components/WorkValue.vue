<script setup>
defineProps({
    total: {
        type: Number,
        required: true
    },
    cards: {
        type: Array,
        required: true
    },
    value: {
        type: String,
        required: true
    },
    cards3: {
        type: Array,
        required: true
    }
})
</script>

<template>
    <div class="work-value" color="value">
        <h4>Achievement</h4>
        <div>
            <div class="work-value-header">
                <span>Card</span><span>Score</span>
            </div>
            <div class="work-value-row">
                <span>{{cards[0]}}</span><span>{{cards3.value[0].rank}}</span>
            </div>
            <div class="work-value-row">
                <span>{{cards[1]}}</span><span>{{cards3.value[5].rank}}</span>
            </div>
            <div class="work-value-total">
                <span></span><span>{{total}}</span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.work-value {
    max-width: 200px;
    background-color: bisque;
}

.work-value h4 {
    padding: 10px;
    text-align: center;
    margin: 0;
}
.work-value-row,
.work-value-total {
    clear: both;
}
.work-value-row span,
.work-value-total span,
.work-value-header span {
    float: left;
    padding: 10px;
    text-align: center;
    width: 50%;
    position: relative;
}

.work-value-row+.work-value-row span+span::before {
    content: "+";
    left: 10px;
    position: absolute;
}

.work-value-total span:last-of-type::before {
    content: "=";
    left: 10px;
    position: absolute;
}

.work-value-header {
    font-weight: bold;
}
</style>
