<script setup>
import { ref } from 'vue';
import { onBeforeMount, reactive } from "@vue/runtime-core";
import { cards2 } from "../App.vue";
import { OnetWebService } from "../main.js";

const valueDescriptions = {
    "Achievement" : "If Achievement is your highest work value, look for jobs that let you use your best abilities. Look for work where you can see the results of your efforts. Explore jobs where you can get the feeling of accomplishment.",
    "Independence" : "If Independence is your highest work value, look for jobs where they let you do things on your own initiative. Explore work where you can make decisions on your own.",
    "Recognition" : "If Recognition is your highest work value, explore jobs with good possibilities for advancement. Look for work with prestige or with the potential for leadership.",
    "Relationships" : "If Relationships is your highest work value, look for jobs where your co-workers are friendly. Look for work that lets you be of service to others. Explore jobs that do not make you do anything that goes against your sense of right and wrong.",
    "Support" : "If Support is your highest work value, look for jobs where the company stands behind its workers and where the workers are comfortable with management’s style of supervision. Explore work in companies with a reputation for competent, considerate, and fair management.",
    "Working Conditions" : "If Working Conditions is your highest work value, consider pay, job security, and good working conditions when looking at jobs. Look for work that suits your work style. Some people like to be busy all the time, or work alone, or have many different things to do. Explore jobs where you can take best advantage of your particular work style."
}
const values = {
    "Achievement" : ["A", "F"],
    "Independence" : ["I", "M", "T"],
    "Recognition" : ["D", "E", "L"],
    "Relationships" : ["H", "K", "O"],
    "Support" : ["B", "P", "Q"],
    "Working Conditions" : ["C", "G", "J", "N", "R", "S"]
}
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
let currentZone = ref(null); // Sets the radio box values.
let futureZone = ref(null); // Sets the radio box values.

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
})

function fetchOccupations(zone, value) {
    let onet_ws = new OnetWebService("digitalspaces_dev");
    onet_ws.call('mnm/job_preparation/' + zone, 'start=1&end=200', function(vinfo) {
        vinfo.career.forEach((item) => {
            onet_ws.call(`online/occupations/${item.code}/details/work_values/`, null, function(winfo) {
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
</script>

<template>
    <p>Review your scores, then select your current and future job zone. Press "See Jobs" for a personalized listing of jobs that suit your values and level of education, experience and training.</p>

    <div id="display-view">
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
            <h3>{{ workValuesSorted.value[0][0] }}</h3>
            <p>{{ valueDescriptions[workValuesSorted.value[0][0]] }}</p>
            <h3>{{ workValuesSorted.value[1][0] }}</h3>
            <p>{{ valueDescriptions[workValuesSorted.value[1][0]] }}</p>
        </div>

        <div id="job-zones">
            <h3>Job Zones</h3>
            <p>A Job Zone is a group of occupations that are similar in these ways:</p>
            <ul>
                <li>How most people get into the job</li>
                <li>How much overall experience people need to do the job</li>
                <li>How much education people need to do the job</li>
                <li>How much on-the-job training people need to do the job</li>
            </ul>
            <dl>
                <dt>Job Zone 1</dt>
                <dd>Occupations that need <i>Little</i> or <i>No</i> preparation.</dd>
                <dt>Job Zone 2</dt>
                <dd>Occupations that need <i>Some</i> preparation.</dd>
                <dt>Job Zone 3</dt>
                <dd>Occupations that need <i>Medium</i> preparation.</dd>
                <dt>Job Zone 4</dt>
                <dd>Occupations that need <i>Considerable</i> preparation.</dd>
                <dt>Job Zone 5</dt>
                <dd>Occupations that need <i>Extensive</i> preparation.</dd>
            </dl>
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

#highest-work-values,
#job-zones {
    font-size: 18px;
    h3 {
        margin-top: 5px;
    }
}

#job-zones {
    dt {
        font-weight: 700;
    }
    dd {
        margin-left: 20px;
    }
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
