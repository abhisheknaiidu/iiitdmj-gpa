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
        <option v-for="i in 8" :value="i" :key="i">{{i}} Completed 🔥</option>
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
    <h4>{{captions}}</h4>
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
    captions() {
      if (this.totalCPI <= 10 && this.totalCPI > 8.5) {
        return 'Can expect to go to JAPAN 🇯🇵 🤓';
      } if (this.totalCPI <= 8.5 && this.totalCPI > 7.8) {
        return ' Macchaa! Rocked it 😎';
      } if (this.totalCPI <= 7.8 && this.totalCPI > 7) {
        return ' Cool, great score 🥂 ';
      } if (this.totalCPI <= 7 && this.totalCPI > 6) {
        return 'Needs to put extra effort 🔨';
      } if (this.totalCPI <= 6) {
        return 'Padh lo thoda bro 😐';
      }
      return 'It Seems, you have entered the wrong value ❌';
    },
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
