<template>
  <div class="vic-frame">
    <div class="vic-container" :style="base">
      <span class="vic-remarks">hello world</span>
      <canvas ref="vicBackground" :width="base.width" :height="base.height"></canvas>
    </div>
  </div>
</template>

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
        width: '400px',
        height: '300px'
      },
      img: {
        path: '',
        loading: false
      },
      vicBackground: {
        canvas: null,
        context: null
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
    // 更新base数据
    updateBaseFromOptions() {
      if (this.options && this.options.base) {
        this.base = { ...this.base, ...this.handlerBaseData(this.options.base) };
        this.img = { ...this.img, ...this.options.img };
      }
    },
    // 过滤base数据
    handlerBaseData(data) {
      const result = { ...data };
      this.addPxToDimensions(result, 'width');
      this.addPxToDimensions(result, 'height');
      return result;
    },
    //如果值没有带单位，则加上 px
    addPxToDimensions(result, key) {
      if (result[key] && !/px$/.test(result[key])) {
        result[key] += 'px';
      }
      return result;
    },
    // 初始化画布
    initCanvas() {
      console.log("初始化画布")
      this.vicBackground.canvas = this.$refs.vicBackground;
      this.vicBackground.context = this.vicBackground.canvas.getContext('2d');
      // const img = new Image();
      // img.onload = function () {
      // }
    }
  },
  mounted() {
    // 初始化画布
    this.initCanvas();
  },
}
</script>

<style>
.vic-frame {
  background-color: darkgrey;
  display: flex;
  /* Safari */
  display: -webkit-flex;
  justify-content: center;
}

.vic-container {
  background-color: #ffc;
  position: relative;

  /* width: 300px;
  height: 300px; */
  .vic-remarks {
    position: absolute
  }
}
</style>
