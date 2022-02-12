<script setup>
import Card from '@/components/Card.vue'
import CardColumn from '@/components/CardColumn.vue'

const cards = {
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
}

/*const cards2 = [
    {
        letter: "A",
        desc: "I make use of my abilities."
    },
    {"B" : "I would be treated fairly by the company."},
    {"C" : "I could be busy all the time."},
    {"D" : "the job would provide opportunity for advancement."},
    {"E" : "I could give directions and instructions to others."},
    {"F" : "the work could give me a feeling of accomplishment."},
    {"G" : "my pay would compare well with that of other workers."},
    {"H" : "my co-workers would be easy to get along with."},
    {"I" : "I could try out my own ideas."},
    {"J" : "I could work alone."},
    {"K" : "I would never be pressured to do things that go against my sense of right and wrong."},
    {"L" : "I could receive recognition for the work I do."},
    {"M" : "I could make decisions on my own."},
    {"N" : "the job would provide for steady employment."},
    {"O" : "I could do things for other people."},
    {"P" : "I have supervisors who would back up their workers with management."},
    {"Q" : "I have supervisors who train their workers well."},
    {"R" : "I could do something different every day."},
    {"S" : "the job would have good working conditions."},
    {"T" : "I could plan my work with little supervision."}
]

const types = {
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
        <div id="col-start">
            <Card v-for="(value, key) in cards" :id="key" :desc="value" :key="key" />
        </div>
        
        <CardColumn rank="5" />
        <CardColumn rank="4" />
        <CardColumn rank="3" />
        <CardColumn rank="2" />
        <CardColumn rank="1" />
    </div>
</template>

<style scoped>
#columns-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: auto;
    max-width: 1400px;
}

.col, #col-start {
    background-color: yellow;
    width: calc(20% - 20px);
}
</style>
