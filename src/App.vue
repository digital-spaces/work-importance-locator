<script>
export let cards2 = reactive({value:[
    {
        letter: "A",
        desc: "I make use of my abilities.",
        rank: 0,
        value: "Achievement"
    },
    {
        letter: "B",
        desc: "I would be treated fairly by the company.",
        rank: 0,
        value: "Support"
    },
    {
        letter: "C",
        desc: "I could be busy all the time.",
        rank: 0,
        value: "Working Conditions"
    },
    {
        letter: "D",
        desc: "the job would provide opportunity for advancement.",
        rank: 0,
        value: "Recognition"
    },
    {
        letter: "E",
        desc: "I could give directions and instructions to others.",
        rank: 0,
        value: "Recognition"
    },
    {
        letter: "F",
        desc: "the work could give me a feeling of accomplishment.",
        rank: 0,
        value: "Achievement"
    },
    {
        letter: "G",
        desc: "my pay would compare well with that of other workers.",
        rank: 0,
        value: "Working Conditions"
    },
    {
        letter: "H",
        desc: "my co-workers would be easy to get along with.",
        rank: 0,
        value: "Relationships"
    },
    {
        letter: "I",
        desc: "I could try out my own ideas.",
        rank: 0,
        value: "Independence"
    },
    {
        letter: "J",
        desc: "I could work alone.",
        rank: 0,
        value: "Working Conditions"
    },
    {
        letter: "K",
        desc: "I would never be pressured to do things that go against my sense of right and wrong.",
        rank: 0,
        value: "Relationships"
    },
    {
        letter: "L",
        desc: "I could receive recognition for the work I do.",
        rank: 0,
        value: "Recognition"
    },
    {
        letter: "M",
        desc: "I could make decisions on my own.",
        rank: 0,
        value: "Independence"
    },
    {
        letter: "N",
        desc: "the job would provide for steady employment.",
        rank: 0,
        value: "Working Conditions"
    },
    {
        letter: "O",
        desc: "I could do things for other people.",
        rank: 0,
        value: "Relationships"
    },
    {
        letter: "P",
        desc: "I have supervisors who would back up their workers with management.",
        rank: 0,
        value: "Support"
    },
    {
        letter: "Q",
        desc: "I have supervisors who train their workers well.",
        rank: 0,
        value: "Support"
    },
    {
        letter: "R",
        desc: "I could do something different every day.",
        rank: 0,
        value: "Working Conditions"
    },
    {
        letter: "S",
        desc: "the job would have good working conditions.",
        rank: 0,
        value: "Working Conditions"
    },
    {
        letter: "T",
        desc: "I could plan my work with little supervision.",
        rank: 0,
        value: "Independence"
    }
]});
</script>

<script setup>
import { reactive } from "vue";
import { RouterView } from 'vue-router';
//import CardSort from '@/components/CardSort.vue';
</script>

<template>
  <div className="App">
    <main>
      <h1>Work Importance Locator</h1>
      <RouterView />
      <!--<CardSort />-->
    </main>

    <footer>
      <p>This page includes information from the <a href="https://www.onetcenter.org/tools.html">O*NET Career Exploration Tools</a> by the U.S. Department of Labor, Employment and Training Administration (USDOL/ETA). Used under the <a href="/license_tools.html">O*NET Tools Developer License</a>. O*NET&reg; is a trademark of USDOL/ETA. Digital Spaces has modified all or some of this information. USDOL/ETA has not approved, endorsed, or tested these modifications.</p>
      <p>Developer's note: the contents and purpose(s) of these tools have not been modified, only their format. The content, purpose(s) and functionality are otherwise identical to the paper-based WIL tool.</p>
      <p>This site incorporates information from <a href="https://services.onetcenter.org/">O*NET Web Services</a> by the U.S. Department of Labor, Employment and Training Administration (USDOL/ETA).</p>
    </footer>
  </div>
</template>

<style lang="scss">
@import url("@/assets/base.css");
$page-width: 1440px;
$text-color: #333;
$footer-bg: #eee;
$footer-text-size: 10px;

* {
  box-sizing: border-box;
}

main {
  color: $text-color;
  margin: auto;
  max-width: $page-width;
  h1, h2, h3, h4, h5, h6 {
      font-weight: 700;
  }
}

footer {
  background-color: $footer-bg;
  font-size: $footer-text-size;
  margin-top: 30px;
  padding: 40px 0;
  p {
    margin: 5px auto;
    max-width: $page-width;
  }
}

</style>
