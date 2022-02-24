<script setup>
import Card from '@/components/Card.vue'
import { computed, /*reactive*/ } from "vue";
import { cards2 } from "../App.vue";

//import CardColumn from '@/components/CardColumn.vue'

/*const cards = {
    "A" : "I make use of my abilities.",
    "B" : "I would be treated fairly by the company.",
    "C" : "I could be busy all the time.",
    "D" : "the job would provide opportunity for advancement.",
    "E" : "I could give directions and instructions to others.",
    "F" : "the work could give me a feeling of accomplishment.",
    "G" : "my pay would compare well with that of other workers.",
    "H" : "my co-workers would be easy to get along with.",
    "I" : "I could try out my own ideas.",
    "J" : "I could work alone.",
    "K" : "I would never be pressured to do things that go against my sense of right and wrong.",
    "L" : "I could receive recognition for the work I do.",
    "M" : "I could make decisions on my own.",
    "N" : "the job would provide for steady employment.",
    "O" : "I could do things for other people.",
    "P" : "I have supervisors who would back up their workers with management.",
    "Q" : "I have supervisors who train their workers well.",
    "R" : "I could do something different every day.",
    "S" : "the job would have good working conditions.",
    "T" : "I could plan my work with little supervision."
}*/

/*var cards2 = reactive({value:[
    {
        letter: "A",
        desc: "I make use of my abilities.",
        rank: 0
    },
    {
        letter: "B",
        desc: "I would be treated fairly by the company.",
        rank: 0
    },
    {
        letter: "C",
        desc: "I could be busy all the time.",
        rank: 0
    },
    {
        letter: "D",
        desc: "the job would provide opportunity for advancement.",
        rank: 0
    },
    {
        letter: "E",
        desc: "I could give directions and instructions to others.",
        rank: 0
    },
    {
        letter: "F",
        desc: "the work could give me a feeling of accomplishment.",
        rank: 0
    },
    {
        letter: "G",
        desc: "my pay would compare well with that of other workers.",
        rank: 0
    },
    {
        letter: "H",
        desc: "my co-workers would be easy to get along with.",
        rank: 0
    },
    {
        letter: "I",
        desc: "I could try out my own ideas.",
        rank: 0
    },
    {
        letter: "J",
        desc: "I could work alone.",
        rank: 0
    },
    {
        letter: "K",
        desc: "I would never be pressured to do things that go against my sense of right and wrong.",
        rank: 0
    },
    {
        letter: "L",
        desc: "I could receive recognition for the work I do.",
        rank: 0
    },
    {
        letter: "M",
        desc: "I could make decisions on my own.",
        rank: 0
    },
    {
        letter: "N",
        desc: "the job would provide for steady employment.",
        rank: 0
    },
    {
        letter: "O",
        desc: "I could do things for other people.",
        rank: 0
    },
    {
        letter: "P",
        desc: "I have supervisors who would back up their workers with management.",
        rank: 0
    },
    {
        letter: "Q",
        desc: "I have supervisors who train their workers well.",
        rank: 0
    },
    {
        letter: "R",
        desc: "I could do something different every day.",
        rank: 0
    },
    {
        letter: "S",
        desc: "the job would have good working conditions.",
        rank: 0
    },
    {
        letter: "T",
        desc: "I could plan my work with little supervision.",
        rank: 0
    }
]});*/

/*function rankZero() {
    return cards2.filter(item => item.rank === 0);
}
function rankOne() {
    return cards2.filter(item => item.rank === 1);
}
function rankTwo() {
    return cards2.filter(item => item.rank === 2);
}
function rankThree() {
    return cards2.filter(item => item.rank === 3);
}
function rankFour() {
    return cards2.filter(item => item.rank === 4);
}
function rankFive() {
    return cards2.filter(item => item.rank === 5);
}*/

//let rankZero = cards2.filter(item => item.rank == 0);

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

/*let rankZero = [];
let rankFive = [];
let rankFour = [];
let rankThree = [];
let rankTwo = [];
let rankOne = [];*/

function onDrop(e, list) {
    //console.log(cards2.value);
    const itemID = e.dataTransfer.getData('itemID');
    const item = this.cards2.value.find(item => item.letter == itemID);
    item.rank = list;
    
    //console.log("test" + list);
    //console.log(item);
    //console.log(cards2.value);
    //console.log(rankZero.value);
    //console.log(cards2.value.filter(item => item.rank == 5));
    //console.log(rankZero.value.length);
}

/*onMounted(()=> {
    console.log(rankZero);
    rankZero = cards2.filter(item => item.rank == 0);
    console.log(rankZero);
})*/

/*const types = {
    "Achievement" : ["A", "F"],
    "Independence" : ["I", "M", "T"],
    "Recognition" : ["D", "E", "L"],
    "Relationships" : ["H", "K", "O"],
    "Support" : ["B", "P", "Q"],
    "Working Conditions" : ["C", "G", "J", "N", "R", "S"]
}*/

//const myMap = new Map(Object.entries(cards));
//let cardsArray = [];
</script>

<template>
    <div id="columns-container">
        <div id="col-start" :rank=0 @drop="onDrop($event, 0)" @dragover.prevent @dragenter.prevent>
            <Card v-for="item in rankZero" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
            <!--<Card v-for="item in cards2" :id="item.letter" :desc="item.desc" :key="item.letter" />-->
        </div>

        <div 
            className='col' 
            :rank=5 
            @drop="onDrop($event, 5)" 
            @dragover.prevent 
            @dragenter.prevent 
            :valid="rankFive.length==4 ? 'yes' : 'no'"
        >
            <h2>{{rankFive.length}} / 4</h2>
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
            <h2>{{rankFour.length}} / 4</h2>
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
            <h2>{{rankThree.length}} / 4</h2>
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
            <h2>{{rankTwo.length}} / 4</h2>
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
            <h2>{{rankOne.length}} / 4</h2>
            <Card v-for="item in rankOne" :id="item.letter" :desc="item.desc" :key="item" :card="item" />
        </div>
        <!--<CardColumn :rank=5 :cards="rankFive()" />
        <CardColumn :rank=4 :cards="rankFour()" />
        <CardColumn :rank=3 :cards="rankThree()" />
        <CardColumn :rank=2 :cards="rankTwo()" />
        <CardColumn :rank=1 :cards="rankOne()" />-->
        <RouterLink to="/results" v-if="rankFive.length == 4 && rankFour.length == 4 && rankThree.length == 4 && rankTwo.length == 4 && rankOne.length == 4" class="submit">Submit</RouterLink>
        <span v-else class="submit">About</span>
    </div>
</template>

<style scoped lang="scss">
$col-color: yellow;

#columns-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: auto;
    max-width: 1400px;
}

.col, #col-start {
    background-color: $col-color;
    margin: 10px;
    padding: 10px;
    width: calc(20% - 20px);
}
</style>
