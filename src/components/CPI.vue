<template>
  <div>
      <div class="nav">
        <div class="branch">
        <label>Branch</label>
        <button @click="selected='!selectedB',selectedBranch='cse'"
                :class="[selected ? 'active' : '']" > CSE
        </button>
        <button @click="selected='!selectedB',selectedBranch='ece'"
                :class="[selected ? 'active' : '']"> ECE
        </button>
        <button @click="selected='!selectedB',selectedBranch='me'"
                :class="[selected ? 'active' : '']"> ME
        </button>
        </div>
    <div class="semester">
        <label>Semesters Completed</label>
        <select v-model.number="selectedSemester" class="smaller">
        <option v-for="i in 8" :value="i" :key="i">{{i}} Done</option>
        </select>
        </div>
    </div>
    <div class="course-list">
        <div class="courseitem small" v-for="i in selectedSemester" :key="i">
            <p>Semester {{i}}</p>
            <input type="number" v-model="spis[i]" placeholder="placeholder(i)" max="10" min="0">
        </div>
    </div>
    <hr v-if="totalScore">
    <div class="verdict" v-if="totalScore">
    <h3>{{animatedResult}}<span class="outta" v-if="totalScore">/10</span></h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CPI',
  data() {
    return {
    //   credits,
      tweenedNumber: 0,
      selectedSemester: 4,
      selected: false,
      selectedBranch: 'cse',
      spis: [],
    };
  },
  methods: {
    selectedB() {
      this.selected = !this.selected;
    },
  },

};
</script>
<style lang="scss">

.small {
  justify-content: center;
}
.smaller {
  background-position: 83% center !important;
}

</style>
