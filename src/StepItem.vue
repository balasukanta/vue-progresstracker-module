<template>
  <li v-on:mouseover="myHover" class="progress-step" :class="{'is-active': isActive, 'is-complete': isComplete }">
    <span :class="{myCustomClass: myCustomClass, tooltip: tooltip, 'is-tooltip-top': tooltipTop}" v-bind:data-tooltip="data" class="progress-marker">{{ marker }}</span>
    <span  class="progress-text" v-if="title">
      <h4 class="progress-title">{{ title }}</h4>{{ text }}
      <slot></slot>
    </span>
  </li>
</template>

<script>
import '../../../client/assets/scss/tooltip.scss'
export default {
  data () {
    return {
      data: '',
      tooltip: false,
      tooltipTop: false,
      myCustomClass: false
    }
  },
  props: {
    isActive: Boolean,
    isComplete: Boolean,
    marker: {
      type: String,
      default: ''
    },
    kind: String,
    title: String,
    text: String
  },

  computed: {
    index () {
      return this.$parent.$stepItems.indexOf(this)
    }
  },
  created () {
    this._isStepItem = true
  },
  mounted () {
    this.myMethod ()
  },
  methods: {
    myMethod () {
      if(this.$parent.$stepItems.indexOf(this) === 0) {
        this.myCustomClass = true
      }
    },
    myHover () {
      this.tooltip = true
      this.tooltipTop = true
      if(this.$parent.$stepItems.indexOf(this) === 0) {
        this.tooltip = false
        this.tooltipTop = false
        this.data = 'Mobilise'
      }
      if(this.$parent.$stepItems.indexOf(this) === 1) {
        this.data = 'Assess'
      }
      if(this.$parent.$stepItems.indexOf(this) === 2) {
        this.data = 'Design'
      }
      if(this.$parent.$stepItems.indexOf(this) === 3) {
        this.data = 'Implement'
      }
      if(this.$parent.$stepItems.indexOf(this) === 4) {
        this.data = 'Sustain'
      }
    }
  }
}
</script>
<style>
.myCustomClass {
  width:70px!important;
  height:30px!important;
}
</style>
