<template>
  <div id="app">
    <div class="background"><img src=""></div>
    <div class="content">
      <h1>IIITDMJ GPA Calculator</h1>
      <div class="main">
      <div class="selection">
          <button @click="spi=true" :class="[spi ? 'active' : '']" >
            Semester Performance Index (SPI)
          </button>
          <button @click="spi=false" :class="[spi ? '' : 'active']">
            Cumulative Performance Index (CPI)
          </button>
      </div>
      <div class="spibox" v-if="spi">
        <SPI/>
      </div>
      <div class="cpibox" v-if="!spi">
        <CPI/>
      </div>
    </div>
    </div>
    <div class="cui-embed" data-cui-uid="oWD33V"
    data-cui-avatar="https://images.typeform.com/images/74GFgzxk2UPM"
    data-cui-mode="pill" data-cui-pill-button-color="#E26D5A">
    </div>
    <footer><a href="https://github.com/abhisheknaiidu/gradecalc" target="_blank">Made with 💕 by </a> <a href="https://github.com/abhisheknaiidu/" target="_blank">  abhisheknaiidu 😷 </a></footer>
  </div>
</template>

<script>
import SPI from '@/components/SPI.vue';
import CPI from '@/components/CPI.vue';

export default {
  name: 'App',
  components: {
    SPI,
    CPI,
  },
  data() {
    return {
      spi: true,
    };
  },
};

</script>

<style scoped lang="scss">
@import './styles/app.scss';

</style>
