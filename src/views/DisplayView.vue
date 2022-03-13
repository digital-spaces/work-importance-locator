<script setup>
import { ref } from 'vue';
import { onBeforeMount, reactive } from "@vue/runtime-core";
import { cards2 } from "../App.vue";
import { OnetWebService } from "../main.js";

let currentZone = ref(null);
let futureZone = ref(null);

let workValues = {
    "Achievement" : 0,
    "Independence" : 0,
    "Recognition" : 0,
    "Relationships" : 0,
    "Support" : 0,
    "Working Conditions" : 0
};

let workValuesSorted = reactive({value:[]});

let jobs = reactive({value:[]});

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

    //fetchOccupations(1, "Relationships");
})

function fetchOccupations(zone, value) {
    let onet_ws = new OnetWebService("digitalspaces_dev");
    onet_ws.call('mnm/job_preparation/' + zone, 'start=1&end=200', function(vinfo) {
        //console.log(vinfo.career);
        vinfo.career.forEach((item) => {
            //console.log(item.code);
            onet_ws.call(`online/occupations/${item.code}/details/work_values/`, null, function(winfo) {
                //console.log(winfo.element[0].name);
                //console.log(item);
                //console.log(winfo.element[0].name);
                if (winfo.element[0].name == value) {
                    jobs.value.push([item.code, item.title]);
                }
            });
        });
    })
}

function allOccupations(fZone, cZone, pValue, sValue) {
    jobs.value = [];
    fetchOccupations(fZone,pValue);
    fetchOccupations(cZone,pValue);
    fetchOccupations(fZone,sValue);
    fetchOccupations(cZone,sValue);
}

function comparator(a, b) {
    if (a[1].toUpperCase() < b[1].toUpperCase()) return -1;
    if (a[1].toUpperCase() > b[1].toUpperCase()) return 1;
    return 0;
}
</script>

<template>
    <p>Review your scores, then select your current and future job zone. Press "See Jobs" for a personalized listing of jobs that suit your values and level of education, experience and training.</p>

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
            <p>Your highest work value is {{ workValuesSorted.value[0][0] }} ({{ workValuesSorted.value[0][1] }}).</p>
            <p>Your second-highest work value is {{ workValuesSorted.value[1][0] }} ({{ workValuesSorted.value[1][1] }}).</p>
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

        <div v-if="currentZone > 0 && futureZone > 0 && currentZone != futureZone">
            <a class="submit" @click="allOccupations(futureZone, currentZone, workValuesSorted.value[0][0], workValuesSorted.value[1][0])">See Jobs</a>
        </div>

        <ul v-if="jobs.value.length > 0" class="jobs">
            <li v-for="job in jobs.value.sort(comparator)" :key="job[0]">
                <a :href="'https://www.onetonline.org/link/summary/' + job[0]">{{job[1]}}</a>
            </li>
        </ul>
    </div>
</template>

<style scoped lang="scss">
@mixin work-value-spans {
    float: left;
    padding: 10px;
    text-align: center;
    width: 50%;
    position: relative;
}

#work-value-worksheet {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: 20px 0px;
}
.work-value {
    max-width: 200px;
    background-color: bisque;
    flex-basis: calc(100%/6);
    h4 {
        padding: 10px;
        text-align: center;
        margin: 0;
    }
    &-row,
    &-total {
        clear: both;
        span {
            @include work-value-spans;
        }
    }
    &-header {
        font-weight: bold;
        span {
            @include work-value-spans;
        }
    }
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

#highest-work-values {
    font-size: 18px;
    input {
        margin: 0 4px 0 10px;
    }
}

.submit {
    padding: 20px 40px;
    text-transform: uppercase;
    background-color: forestgreen;
    display: inline-block;
    color: white;
    margin-top: 10px;
    cursor: pointer;
}

.jobs {
    margin-top: 20px;
    -moz-column-count: 4;
    -moz-column-gap: 20px;
    -webkit-column-count: 4;
    -webkit-column-gap: 20px;
    column-count: 3;
    column-gap: 20px;
    padding-left: 0px;
    li {
        list-style-type: none;
    }
}
</style>
