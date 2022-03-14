<script setup>
import Card from '@/components/Card.vue'
import { computed } from "vue";
import { cards2 } from "../App.vue";

let rankZero = computed({
    get: () => 
        cards2.value.filter(item => item.rank == 0)
});
let rankFive = computed({
    get: () => 
        cards2.value.filter(item => item.rank == 5)
});
let rankFour = computed({
    get: () => 
        cards2.value.filter(item => item.rank == 4)
});
let rankThree = computed({
    get: () => 
        cards2.value.filter(item => item.rank == 3)
});
let rankTwo = computed({
    get: () => 
        cards2.value.filter(item => item.rank == 2)
});
let rankOne = computed({
    get: () => 
        cards2.value.filter(item => item.rank == 1)
});

function onDrop(e, list) {
    const itemID = e.dataTransfer.getData('itemID');
    const item = cards2.value.find(item => item.letter == itemID);
    item.rank = list;
}
</script>

<template>
    <p>A web form adaptation of O*NET's Work Importantance Locator.</p>
    <p>Simply drag your priorities from the first column into the others, from most to least important, then press Submit. Only 4 cards per column.</p>

    <RouterLink to="/results" v-if="rankFive.length == 4 && rankFour.length == 4 && rankThree.length == 4 && rankTwo.length == 4 && rankOne.length == 4" class="submit">Submit</RouterLink>
    <span v-else class="submit">Submit</span>

    <div id="columns-container">
        <div :style="(rankZero.length == 0) ? 'display:none;' : ''" id="col-start" :rank=0 @drop="onDrop($event, 0)" @dragover.prevent @dragenter.prevent>
            <Card v-for="item in rankZero" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
        </div>

        <div 
            className='col' 
            :rank=5 
            @drop="onDrop($event, 5)" 
            @dragover.prevent 
            @dragenter.prevent 
            :valid="rankFive.length==4 ? 'yes' : 'no'"
        >
            <h2>Rank 5</h2>
            <h3>{{rankFive.length}} / 4</h3>
            <Card v-for="item in rankFive" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
        </div>

        <div 
            className='col' 
            :rank=4 
            @drop="onDrop($event, 4)" 
            @dragover.prevent 
            @dragenter.prevent
            :valid="rankFour.length==4 ? 'yes' : 'no'"
        >
            <h2>Rank 4</h2>
            <h3>{{rankFour.length}} / 4</h3>
            <Card v-for="item in rankFour" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
        </div>

        <div 
            className='col' 
            :rank=3 
            @drop="onDrop($event, 3)" 
            @dragover.prevent 
            @dragenter.prevent
            :valid="rankThree.length==4 ? 'yes' : 'no'"
        >
            <h2>Rank 3</h2>
            <h3>{{rankThree.length}} / 4</h3>
            <Card v-for="item in rankThree" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
        </div>

        <div 
            className='col' 
            :rank=2 
            @drop="onDrop($event, 2)" 
            @dragover.prevent 
            @dragenter.prevent
            :valid="rankTwo.length==4 ? 'yes' : 'no'"
        >
            <h2>Rank 2</h2>
            <h3>{{rankTwo.length}} / 4</h3>
            <Card v-for="item in rankTwo" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
        </div>

        <div 
            className='col' 
            :rank=1 
            @drop="onDrop($event, 1)" 
            @dragover.prevent 
            @dragenter.prevent
            :valid="rankOne.length==4 ? 'yes' : 'no'"
        >
            <h2>Rank 1</h2>
            <h3>{{rankOne.length}} / 4</h3>
            <Card v-for="item in rankOne" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
        </div>
    </div>
</template>

<style scoped lang="scss">
$col-bg-invalid: salmon;
$col-bg-valid: lightgreen;
$btn-bg-invalid: gray;
$btn-bg-valid: forestgreen;

#columns-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-left: -10px;
    margin-right: -10px;
}

.col, #col-start {
    background-color: $col-bg-invalid;
    margin: 10px;
    padding: 10px;
    width: calc(20% - 20px);
    border-radius: 4px;
}

.col[valid=yes] {
    background-color: $col-bg-valid;
}

.submit {
    background-color: $btn-bg-valid;
    color: white;
    display: inline-block;
    margin-top: 40px;
    padding: 20px 40px;
    text-decoration: none;
    text-transform: uppercase;
    border-radius: 4px;
}

span.submit {
    background-color: $btn-bg-invalid;
    cursor: not-allowed;
}
</style>
