<template>
  <div 
    class="el-card" 
    :class="shadow ? `is-${shadow}-shadow`: 'is-always-shadow'"
  >
    <div class="el-card__header" v-if="$slots.header || header">
      <slot name="header">{{ header }}</slot>
    </div>
    <div class="el-card__body" :style="bodyStyle">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import { inject, computed, getCurrentInstance} from 'vue';

export default {
  name: 'ElCard',
  data() {
    return {
      mapShadow: ['always', 'hover', 'never']
    }
  },
  props: {
    shadow: {
      type: String,
      default: '',
      // validator: function (value) {
      //   return ['always', 'hover', 'never'].indexOf(value) !== -1
      // }
    },
    header: {
      type: String
    },
    bodyStyle: {
      type: Object,
      default: () => {}
    } 
  },

  setup(props, ctx) {
    const { shadow } = props;
    if (shadow && !this.mapShadow.includes(shadow)) {
      console.warn('shadow参数可选值只有always, hover, never')
    }
  }

}
</script>