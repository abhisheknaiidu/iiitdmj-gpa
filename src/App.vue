<template>
  <div id="app">
    <div class="background"><img src=""></div>
    <div class="content">
      <h1>ABHISHEK</h1>
      <div class="main">
        <div class="cpibox">
        <CPI/>
      </div>
    </div>
    </div>
    <footer><a href="https://github.com/abhisheknaiidu/gradecalc">Hacked by </a> <a href="https://github.com/abhisheknaiidu/">  abhisheknaiidu 😷 </a></footer>
  </div>
</template>

<script>
import CPI from '@/components/CPI.vue';

export default {
  name: 'App',
  components: {
    CPI,
  },
  data() {
    return {
    };
  },
};

</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Chelsea+Market&display=swap');

#app {
  max-height: 100%;
  .background {
    position: fixed;
    top: 0;
    left: 0;
    min-width: 100%;
    max-width: 100%;
    z-index: -999;
    img{
      width: 100%;
    }
  }
  html {
    font-size: 100%;
  }

  .content {
    display: flex;
    flex-direction: column;
    margin-bottom: 100px;
    h1 {
      font-family: 'Chelsea Market', cursive;
      font-size: 2rem;
      color: #93a1a1;
      font-weight: 700;
      text-align: center;
    }
    .main {
      background: #ffffff;
      box-shadow: 0 5px 20px 0 rgba(179, 179, 179, 0.5);
      border-radius: 0.5rem;
    }
    h2 {
      font-family: 'Chelsea Market', cursive;
      color: #93a1a1;
      text-align: center;
      text-align: center;
      font-size: 1.125rem;
      margin: 0.75rem 0 3rem 0;
      line-height: 1.5rem;
    }
    .selection {
      position: relative;
      top: 82px;
      width: 100%;
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      button {
        cursor: pointer;
        width: 50%;
        padding: 0.75rem;
        background: #fff;
        border: none;
        font-family: 'Chelsea Market', cursive;
        font-size: 0.875rem;
        color: #a6a6a6;
        text-transform: uppercase;
        border-bottom: 1px solid transparent;
        letter-spacing: 0.5px;
        transition-timing-function: ease-in-out;
        transition-duration: 0.25s;
        transition-property: all;
        &:focus {
          outline: none;
        }
      }
      .active {
        border-bottom: 1px solid #2d85fd;
        font-family: 'Chelsea Market', cursive;
        font-weight: 700;
        font-size: 0.875rem;
        color: #2d85fd;
        letter-spacing: 0.5px;
      }
    }
  }
  footer {
    padding: 1rem 0;
    text-align: center;
    background: #f9f9f9;
    position: fixed;
    width: 100%;
    z-index: -999;
    bottom: 0;
    a {
      text-decoration: none;
      font-family: 'Chelsea Market', cursive;
      font-size: 12px;
      color: #a19d9d !important;
    }
  }
}
</style>
