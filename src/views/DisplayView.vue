<script setup>
import { onBeforeMount, reactive } from "@vue/runtime-core";
import { cards2 } from "../App.vue";

let workValues = {
    "Achievement" : 0,
    "Independence" : 0,
    "Recognition" : 0,
    "Relationships" : 0,
    "Support" : 0,
    "Working Conditions" : 0
};

let workValuesSorted = reactive({value:[]});

/*const types = {
    "Achievement" : ["A", "F"],
    "Independence" : ["I", "M", "T"],
    "Recognition" : ["D", "E", "L"],
    "Relationships" : ["H", "K", "O"],
    "Support" : ["B", "P", "Q"],
    "Working Conditions" : ["C", "G", "J", "N", "R", "S"]
}*/

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
})
</script>

<template>
    <div id="display-view">
        <!--{{workValuesSorted.value}}<br>
        {{workValuesSorted.value[0]}}<br>
        {{workValuesSorted.value[0][1]}}-->
        <div id="work-value-worksheet">
            <div class="work-value" value="achievement">
                <h4>Achievement</h4>
                <div>
                    <div class="work-value-row">
                        <span>Card</span><span>Score</span>
                    </div>
                    <div class="work-value-row">
                        <span>A</span><span>{{cards2.value[0].rank}}</span>
                    </div>
                    <div class="work-value-row">
                        <span>F</span><span>+{{cards2.value[5].rank}}</span>
                    </div>
                    <div class="work-value-total">
                        <span>Achievement Score</span><span>{{workValues["Achievement"]}}</span>
                    </div>
                </div>
            </div>
        </div>

        <div id="highest-work-values">
            <p>Your highest score: {{ workValuesSorted.value[0][1] }}. Name of work value: {{ workValuesSorted.value[0][0] }}</p>
            <p>Your next highest score: {{ workValuesSorted.value[1][1] }}. Name of work value: {{ workValuesSorted.value[1][0] }}</p>
        </div>
        <!--{{workValues}}-->
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
