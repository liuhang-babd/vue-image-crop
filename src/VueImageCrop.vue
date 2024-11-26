<template>
  <div class="frame">
    <div class="container" :style="">
      <!-- helloworld -->
    </div>
  </div>
</template>
    return {

<script>
export default {
  props: {
    options: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      base: {
        width: 300,
        height: 300
      }
    }
  },
  created() {
    this.updateBaseFromOptions();
  },
  watch: {
    options: {
      handler(newVal, oldVal) {
        console.log('监听到 options 改变了', newVal, oldVal)
        this.updateBaseFromOptions();
      },
      deep: true
    }
  },
  methods: {
    updateBaseFromOptions() {
      if (this.options && this.options.base) {
        this.base = { ...this.base, ...this.options.base };
      }
    }
  }
}
</script>

<style>
.frame {
  background-color: darkgrey;
  display: flex;
  /* Safari */
  display: -webkit-flex;
  justify-content: center;
}

.container {
  background-color: #ffc;
  width: 300px;
  height: 300px;
}
</style>
