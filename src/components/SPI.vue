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
          <input type="text" placeholder="Course Grade" v-model="courseGrades[index]" >
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
      courseCredits: [],
      courseGrades: [],
      tweenedNumber: 0,
    };
  },
  methods: {
    getScore(grade) {
      switch (grade) {
        case 'O':
        case 'o':
          return 10;
        case 'A+':
        case 'a+':
          return 10;
        case 'A':
        case 'a':
          return 9;
        case 'B+':
        case 'b+':
          return 8;
        case 'B':
        case 'b':
          return 7;
        case 'C+':
        case 'c+':
          return 6;
        case 'C':
        case 'c':
          return 5;
        case 'D+':
        case 'd+':
          return 4;
        case 'D':
        case 'd':
          return 3;
        case 'F':
        case 'f':
          return 2;
        default:
          return 0;
      }
    },
  },
  computed: {
    course() {
      return this[this.selectedBranch];
    },
    computeCourseCredits() {
      this.course[this.selectedSemester].forEach((el) => {
        const { courseCredits } = this;
        courseCredits.push(el.courseCredits);
      });
      return this.courseCredits;
    },
    // test() {
    //   return course.courseCredits;
    // },
    semTotal() {
      let score = 0;
      this.courseGrades.forEach((el, index) => {
        const grade = this.getScore(el);
        score += grade * this.courseCredits[index];
      });
      return score;
    },
  },
  watch: {
    selectedSemester() {
      this.courseGrades = [];
      this.courseCredits = [];
    },
    selectedCourse() {
      this.courseGrades = [];
      this.courseCredits = [];
    },
  },
};

</script>

<style scoped lang="scss">

@import '../styles/home.scss';

</style>
