<template>
  <div>
    <div class="progress-stepper">
      <span class="title">Progress:</span>
      
      <div
        v-for="step, i in totalSteps"
        ref="progressSteps"
        :title="`Go to Step ` + [[ step ]]"
        :key="step"
        :class="['step-outside',{
          'active':   stepActive == step,
          'complete': finishedStep(step),
          'no-click': stepActive == 6
        }]">

        <div class="step-inside" @click="goToStep(step)">
          <svg v-if="finishedStep(step)" version="1.1" id="check" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="46px" height="37px" viewBox="0 0 46 37" enable-background="new 0 0 46 37" xml:space="preserve">
            <polygon id="check-icon" fill="" points="0.2230862,22.3627338 14.1432562,36.2812843 45,5.4261613 40.3345947,0.7607598 14.1432562,26.9504795 4.7655683,17.5744114 "/>
          </svg>

          <span v-if="stepActive <= step">
            {{ step }}
          </span>
        </div>
      </div>
    </div>

    <nav>
      <h1 v-html="group"></h1>
      <h2 v-if="navSubGroup">
        {{ service_name | truncate(25) }}
      </h2>
    </nav>
  </div>
</template>

<style lang="scss" scoped>
.progress-stepper {
  position: relative;
  height: 50px;
  max-width: 520px;
  margin: 0 auto;
  padding: 15px 0;
  display: flex;
  flex-direction: row;
  font-size: 18px;
  line-height: 25px;

  span {
    &.title {
      flex: 1 1 10%;
    }
  }

  div {
    position: relative;
    background: #ccc;
    color: $biscay;
    margin: 0 0 0 15px;
    width: 25px;
    height: 25px;
    border-radius: 50%;
    font-size: 14px;
    line-height: 25px;
    text-align: center;

    &.active {

      .step-inside {
        background-color: white;
      }

      &:before {
        position: absolute;
        content: '';
        width: 33px;
        height: 33px;
        border-radius: 50%;
        border: 2px solid white;
        left: -4px;
        top: -4px;
        z-index: 10;
      }
    }

    &.complete {
      cursor: pointer;
      color: white;
      background: $color-green;

      .step-inside {
        background: $color-green;
      }

      &:after {
        background: $color-green;
      }
    }

    &.no-click {
      cursor: default;
    }

    &:first-of-type {
      margin: 0;
    }

    &:last-of-type {
      &:after {
        display: none;
      }
    }

    &:after {
      position: absolute;
      content: '';
      width: 20px;
      height: 2px;
      right: -20px;
      background: #ccc;
      display: block;
      top: 50%;
      transform: translateY(-50%);
    }

    svg {
      position: relative;
      top: 50%;
      left: 50%;
      transform: translate(-50%,-50%);
      width: 15px;
      height: 12px;
      display: block;
      fill: white;
    }
  }
}

nav {
  position: relative;
  padding: 0 0 5px 0;
  display: flex;
  flex-flow: wrap;
  margin: 0 auto;
  max-width: 520px;

  h1 {
    color: white;
    font-size: 28px;
    font-weight: $weight-semi-bold;
    letter-spacing: .5px;
    display: inline-block;
    line-height: 30px;
    width: auto;
  }

  h2 {
    color: white;
    font-size: 18px;
    letter-spacing: .5px;
    position: relative;
    width: 100%;
    margin: 0;
    overflow: hidden;

    &:after {
      position: absolute;
      content: '';
      // bottom: 50%;
      top: 50%;
      transform: translateY(-50%);
      width: 100%;
      height: 1px;
      margin: 0 0 0 15px;
      background-color: white;
    }
  }

  @media only screen
  and (min-device-width : 320px)
  and (max-device-width : 480px) {
    padding: 0;
    width: calc(100% - 40px);

    h1 {
      font-size: 25px;
      line-height: 25px;
    }

    h2 {
      font-size: 20px;
      line-height: 20px;
    }
  }
}
</style>

<script>
import topBar         from './topBar.vue'
import { mapFields }  from 'vuex-map-fields'

export default {
  props: ['stepActive','stepComplete','navSubGroup'],
  components: {
    topBar
  },
  data() {
    return {
      showModal:       false,
      allData:         [],
      hideBackButton:  false,
      
    }
  },
  mounted() {
    this.confirmRoute();
  },
  filters: {
    truncate(string, value) {
      if(string.length >= value) {
        return string.substring(0, value) + '...';
      } else {
        return string
      }
        
    }
  },
  methods: {
    confirmRoute() {
      if(this.$route.path == '/confirm') {
        this.hideBackButton = true;
      }
    },
    goToStep(step) {
      if(this.stepActive != 6) {
        if(step <= this.stepActive){
          if(step == 2){
            this.$router.push(`/${this.stepperPaths[step].path}`)
          } else {
            this.$router.push(this.stepperPaths[step].path)
          }
        }
      }
    },
    finishedStep(step) {
      if(step < this.stepActive)
        return true
    }
  },
  computed: {
    ...mapFields([
      'stepperPaths',
      'totalSteps',
      'serviceInfos.service_group.group',
      'serviceInfos.service_group.service_name',
    ]),
  }
}
</script>