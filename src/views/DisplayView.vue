<script setup>
import { onBeforeMount, reactive } from "@vue/runtime-core";
import { cards2 } from "../App.vue";
import { OnetWebService } from "../main.js";

let workValues = {
    "Achievement" : 0,
    "Independence" : 0,
    "Recognition" : 0,
    "Relationships" : 0,
    "Support" : 0,
    "Working Conditions" : 0
};

let workValuesSorted = reactive({value:[]});

const values = {
    "Achievement" : ["A", "F"],
    "Independence" : ["I", "M", "T"],
    "Recognition" : ["D", "E", "L"],
    "Relationships" : ["H", "K", "O"],
    "Support" : ["B", "P", "Q"],
    "Working Conditions" : ["C", "G", "J", "N", "R", "S"]
}

onBeforeMount(() => {
    cards2.value.forEach((item) => {
        workValues[item.value] += item.rank;
    });
    workValues["Achievement"] *= 3;
    workValues["Independence"] *= 2;
    workValues["Recognition"] *= 2;
    workValues["Relationships"] *= 2;
    workValues["Support"] *= 2;
    console.log(workValues);

    workValuesSorted.value = Object.entries(workValues).sort((a,b) => b[1]-a[1]);
    //console.log(workValuesSorted.value);

    fetchOccupations();
})

function fetchOccupations() {
    let onet_ws = new OnetWebService("digitalspaces_dev");
    onet_ws.call('about', null, function(vinfo) {
        console.log(vinfo);
    });
}
</script>

<template>
    <div id="display-view">
        <!--{{workValuesSorted.value}}<br>
        {{workValuesSorted.value[0]}}<br>
        {{workValuesSorted.value[0][1]}}-->
        <div id="work-value-worksheet">
            <div v-for="item in Object.entries(values)" class="work-value" :value="item[0]" :key="item[0]">
                <h4>{{item[0]}}</h4>
                <div>
                    <div class="work-value-header">
                        <span>Card</span><span>Score</span>
                    </div>
                    <div v-for="card in item[1]" class="work-value-row" :key="card">
                        <span>{{card}}</span><span>{{cards2.value.find(item => item.letter == card).rank}}</span>
                    </div>
                    <div class="work-value-total">
                        <span></span><span>{{workValues[item[0]]}}</span>
                    </div>
                </div>
            </div>
        </div>

        <div id="highest-work-values">
            <p>Your highest score: {{ workValuesSorted.value[0][1] }}. Name of work value: {{ workValuesSorted.value[0][0] }}</p>
            <p>Your next highest score: {{ workValuesSorted.value[1][1] }}. Name of work value: {{ workValuesSorted.value[1][0] }}</p>
            <div>
                <span>Your current job zone: </span>
                <input type="radio" id="curZone1" name="curZone" value="1" v-model="currentZone">
                <label for="curZone1">1</label>

                <input type="radio" id="curZone2" name="curZone" value="2" v-model="currentZone">
                <label for="curZone2">2</label>

                <input type="radio" id="curZone3" name="curZone" value="3" v-model="currentZone">
                <label for="curZone3">3</label>

                <input type="radio" id="curZone4" name="curZone" value="4" v-model="currentZone">
                <label for="curZone4">4</label>

                <input type="radio" id="curZone5" name="curZone" value="5" v-model="currentZone">
                <label for="curZone5">5</label>
            </div>

            <div>
                <span>Your future job zone: </span>
                <input type="radio" id="curZone1" name="futZone" value="1" v-model="futureZone">
                <label for="futZone1">1</label>

                <input type="radio" id="curZone2" name="futZone" value="2" v-model="futureZone">
                <label for="futZone2">2</label>

                <input type="radio" id="curZone3" name="futZone" value="3" v-model="futureZone">
                <label for="futZone3">3</label>

                <input type="radio" id="curZone4" name="futZone" value="4" v-model="futureZone">
                <label for="futZone4">4</label>

                <input type="radio" id="curZone5" name="futZone" value="5" v-model="futureZone">
                <label for="futZone5">5</label>
            </div>
        </div>
        <!--{{workValues}}-->
    </div>
</template>

<style scoped lang="scss">
#display-view {
    max-width: 1440px;
    margin: auto;
}

#work-value-worksheet {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: flex-start;
}
.work-value {
    max-width: 200px;
    background-color: bisque;
    flex-basis: calc(100%/6);
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

#highest-work-values {
    width: 700px;
    margin: auto;
    background-color: beige;
    border: 2px solid red;
}
</style>
