<template>
  <div class="top-bar" ref="tbHeight">
    <div class="container">
      <a :href="logoUrl">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 225 225"><g id="city-logo" data-name="city-logo 2"><g id="logo"><path id="_8" data-name="8" d="M91.07143,0,112.5,21.42857,133.92857,0V42.85714l21.42857-21.42857V64.28571L133.92857,85.71429,112.5,64.28571,91.07143,85.71429,69.64286,64.28571V21.42857L91.07143,42.85714Z" fill="#183365"/><path id="_7" data-name="7" d="M50.30227,35.412,36.72863,21.8378v15.153H21.57622L35.15044,50.56385,21.42857,64.28571H64.28571V21.42857Z" fill="#183365"/><path id="_6" data-name="6" d="M0,133.92857,21.42857,112.5,0,91.07143H42.85714L21.42857,69.64286H64.28571L85.71429,91.07143,64.28571,112.5l21.42858,21.42857L64.28571,155.35714H21.42857l21.42857-21.42857Z" fill="#183365"/><path id="_5" data-name="5" d="M64.28571,160.71429H21.42857L35.412,174.69773,21.8378,188.272H36.99021v15.15183l13.57422-13.57422,13.72128,13.72187Z" fill="#183365"/><path id="_4" data-name="4" d="M133.92857,225,112.5,203.57143,91.07143,225V182.14286L69.64286,203.57143V160.71429l21.42857-21.42858L112.5,160.71429l21.42857-21.42858,21.42857,21.42858v42.85714l-21.42857-21.42857Z" fill="#183365"/><path id="_3" data-name="3" d="M203.57143,160.71429H160.71429v42.85714L174.69773,189.588,188.272,203.1622v-15.153h15.15183l-13.57422-13.57306Z" fill="#183365"/><path id="_2" data-name="2" d="M225,91.07143,203.57143,112.5,225,133.92857H182.14286l21.42857,21.42857H160.71429l-21.42858-21.42857L160.71429,112.5,139.28571,91.07143l21.42858-21.42857h42.85714L182.14286,91.07143Z" fill="#183365"/><path id="_1" data-name="1" d="M189.588,50.30227,203.1622,36.72805h-15.153V21.57622L174.43615,35.15044,160.71429,21.42857V64.28571h42.85714Z" fill="#183365"/></g></g></svg>
      </a>
      <span>uReport -&nbsp;</span>
      <span>City of Bloomington, Indiana</span>

      <a @click="showingDisclaimer(true)">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 45.43269 45.43269" class="info-icon"><g id="info-icon"><path id="icon" fill="#9e9e9e" d="M22.71538,0A22.71635,22.71635,0,1,0,45.43269,22.71538,22.71682,22.71682,0,0,0,22.71538,0Zm4.72885,35.20577q-1.75385.69231-2.79808,1.05385a7.38179,7.38179,0,0,1-2.42692.36346,4.83681,4.83681,0,0,1-3.30192-1.03654,3.34483,3.34483,0,0,1-1.175-2.62885,9.54777,9.54777,0,0,1,.08654-1.26731c.05961-.43077.15384-.91538.28269-1.45961L19.575,25.06154c.12885-.49616.24038-.96731.32885-1.40577a6.23332,6.23332,0,0,0,.13076-1.21731,1.87475,1.87475,0,0,0-.40769-1.37885,2.3159,2.3159,0,0,0-1.56346-.38654A4.10309,4.10309,0,0,0,16.9,20.84615c-.39423.12115-.73654.23077-1.01731.33846l.38654-1.59231q1.43653-.58557,2.75-1.00192A8.1244,8.1244,0,0,1,21.5,18.17115a4.74674,4.74674,0,0,1,3.25385,1.01923,3.38634,3.38634,0,0,1,1.1423,2.64615q0,.3375-.07884,1.18654a7.94007,7.94007,0,0,1-.29231,1.55962l-1.45577,5.15384c-.11923.41346-.225.88654-.32115,1.41539a7.48429,7.48429,0,0,0-.14039,1.20384,1.729,1.729,0,0,0,.45962,1.4,2.57282,2.57282,0,0,0,1.59038.37308,4.613,4.613,0,0,0,1.20385-.18654,6.844,6.844,0,0,0,.97307-.32692Zm-.25769-20.91923a3.47445,3.47445,0,0,1-2.45192.94615,3.51063,3.51063,0,0,1-2.46154-.94615,3.02046,3.02046,0,0,1-1.025-2.29423,3.05093,3.05093,0,0,1,1.025-2.3,3.48546,3.48546,0,0,1,2.46154-.95577,3.44641,3.44641,0,0,1,2.45192.95577,3.0982,3.0982,0,0,1,0,4.59423Z"/></g></svg>
      </a>
      <disclaimer :showDisclaimer="showDisclaimer" />
    </div>
  </div>
</template>

<script>
import disclaimer from './disclaimer.vue'

export default {
  components: {
    disclaimer
  },
  data() {
    return {
      showDisclaimer: false,
      logoUrl:        process.env.LOGO_URL,
      topBarHeight:   ''
    }
  },
  mounted() {
    this.tbHeight();
  },
  methods: {
    showingDisclaimer(val) {
      this.showDisclaimer = val;
    },
    tbHeight() {
      this.topBarHeight = this.$refs.tbHeight.clientHeight;
      return this.$store.commit('storeTopBarHeight', this.topBarHeight)
    }
  }
}
</script>

<style lang="scss" scoped>
.top-bar {
  z-index: 100000;
  position: fixed;
  top: 0;
  background: white;
  border-bottom: 2px solid darken(white, 20%);
  width: 100%;
  padding: 10px 0;
  color: $biscay;
  font-size: 18px;

  .container {
    position: relative;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    margin: 0 auto;
    max-width: 520px;
    width: 100%;

    a {
      &:first-of-type {
        display: block;
        width: 30px;
        height: 30px;
        margin: 0 10px 0 0;
      }

      &:last-of-type {
        cursor: pointer;
        margin-left: auto;

        svg {
          display: block;
          width: 20px;
          height: 20px;
        }
      }
    }
  }

  @media only screen
  and (min-device-width : 320px)
  and (max-device-width : 480px) {
    .container {
      width: calc(100% - 40px);

      span {
        font-size: 14px;
      }
    }
  }
}
</style>