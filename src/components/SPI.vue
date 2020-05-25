<template>
  <div>
    <div class="nav">
        <div class="branch">
        <label>Branch</label>
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
        <label>Semester</label>
        <select v-model.number="selectedSemester">
        <option v-for="i in 4" :value="i-1" :key="i">Semester {{i}}</option>
        </select>
        </div>
    </div>
    <table class="course-list">
    <tr v-for="(course,index) in course[selectedSemester]" :key="course.id" class="course">
      <td class="name">{{course.courseName}}</td>
        <td>
          <input type="text" placeholder="Course Grade" v-model="courseGrades[index]"  >
        </td>
    </tr>
    </table>
    <hr v-if="totalCPI">
    <div class="result" v-if="totalCPI">
    <h4>{{showMessage}}</h4>
    <h3>{{totalCPI}}<span class="outof" v-if="totalCPI">/10</span></h3>
    </div>
  </div>
</template>

<script>

import cse from '../../static/cse.json';

export default {
  name: 'SPI',
  data() {
    return {
      cse,
      selectedBranch: 'cse',
      selectedSemester: 0,
      courseGrades: [],
      tweenedNumber: 0,
    };
  },
  computed: {
    course() {
      return this[this.selectedBranch];
    },
  },
};

</script>

<style scoped lang="scss">

@import '../styles/home.scss';

</style>
