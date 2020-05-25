/* eslint-disable */
<template>
  <div>
      <div class="nav">
        <div class="branch">
        <label>Branch 📚</label>
        <button @click="selectedBranch='cse'"
                :class="{active: selectedBranch === 'cse' }" > CSE
        </button>
        <button @click="selectedBranch='ece'"
                :class="{active: selectedBranch === 'ece' }"> ECE
        </button>
        <button @click="selectedBranch='me'"
                :class="{active: selectedBranch === 'me' }"> ME
        </button>
        </div>
    <div class="semester">
        <label>Semesters Done 🎉</label>
        <select v-model.number="selectedSemester" class="smaller">
        <option v-for="i in 8" :value="i" :key="i">{{i}} Completed</option>
        </select>
        </div>
    </div>
    <div class="course-list">
        <div class="courseitem small" v-for="i in selectedSemester" :key="i">
            <p>Semester {{i}}</p>
            <input type="number" step=0.1 v-model="spis[i]"
                   :placeholder="textfield(i)" max="10" min="0">
        </div>
    </div>
    <hr v-if="totalScore">
    <div class="result" v-if="totalScore">
    <h3>{{}}<span class="outta" v-if="totalScore">/10</span></h3>
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
      tweenedNumber: 0,
      selectedSemester: 4,
      selectedBranch: 'cse',
      spis: [],
    };
  },
  methods: {
    textfield(i) {
      return `SPI of Semester ${i}`;
    },
  },
  computed: {
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
</style>
