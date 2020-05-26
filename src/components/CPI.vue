/* eslint-disable */
<template>
  <div>
      <div class="nav">
        <div class="branch">
        <label>Branch 📚</label>
        <button @click="selectedBranch='cse'"
                :class="{active: selectedBranch === 'cse' }" > CSE 💻
        </button>
        <button @click="selectedBranch='ece'"
                :class="{active: selectedBranch === 'ece' }"> ECE 💡
        </button>
        <button @click="selectedBranch='me'"
                :class="{active: selectedBranch === 'me' }"> ME 🤖
        </button>
        </div>
    <div class="semester">
        <label>Semesters Done 🎉</label>
        <select v-model.number="selectedSemester" class="smaller">
        <option v-for="i in 4" :value="i" :key="i">{{i}} Completed 🔥</option>
        </select>
        </div>
    </div>
    <div class="course-list">
        <div class="courseitem center" v-for="i in selectedSemester" :key="i">
            <p>Semester {{i}}</p>
            <input type="number" step=0.1 v-model="spis[i]"
                   :placeholder="textfield(i)" max="10" min="0">
        </div>
    </div>
    <hr v-if="totalCPI">
    <div class="result" v-if="totalCPI">
    <h3>{{totalCPI}}<span class="outof" v-if="totalCPI">/10</span></h3>
    </div>
  </div>
</template>

<script>
import credits from '../../static/credits.json';

export default {
  name: 'CPI',
  data() {
    return {
      credits,
      selectedSemester: 4,
      selectedBranch: 'cse',
      spis: [],
    };
  },
  methods: {
    textfield(i) {
      return `SPI of Semester ${i}`;
    },
    getSemCredit(sem) {
      let branch = 0;
      if (this.selectedBranch === 'ece') {
        branch = 1;
      } else if (this.selectedBranch === 'me') {
        branch = 2;
      }
      // eslint-disable-next-line
      return parseInt(credits[`sem${sem}`][branch]);
    },
    calc(num) {
      let numstr = num.toString();
      numstr = numstr.slice(0, numstr.indexOf('.') + 4);
      return Number(numstr);
    },
  },
  computed: {
    // test() {
    //   return this.getSemCredit(3);
    // },
    totalCPI() {
      let totalCredits = 0;
      let obtainedCredits = 0;
      this.spis.forEach((value, index) => {
        totalCredits += this.getSemCredit(index);
        obtainedCredits += this.getSemCredit(index) * value;
      });
      const cpi = obtainedCredits / totalCredits;

      return this.calc(cpi);
    },
  },
  watch: {
    selectedSemester() {
      this.spis = [];
    },
  },
};

</script>
<style scoped lang="scss">

@import '../styles/home.scss';

.center {
  justify-content: center;
}
</style>
