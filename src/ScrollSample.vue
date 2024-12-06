<template>
  <div class="scroll-container" ref="scrollContainer">
    <ul class="scroll-content">
      <li v-for="(item, index) in items" :key="index">{{ item }}</li>
      <!-- Clone the items to create a seamless effect -->
      <li v-for="(item, index) in items" :key="index + items.length">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    props: {},
    data() {
      return {
        items: ['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5'],
        isScrolling: false,
        scrollInterval: null,
      }
    },
    created() {},
    watch: {},
    methods: {
      startScroll() {
        let container = this.$refs.scrollContainer;
        let content = container.querySelector('.scroll-content');
        let itemHeight = container.querySelector('li').clientHeight;

        this.scrollInterval = setInterval(() => {
          if (!this.isScrolling) {
            this.isScrolling = true;
            content.style.transform = `translateY(-${itemHeight}px)`;
            setTimeout(() => {
              // 将第一项移动到列表末尾并重置位置
              content.appendChild(content.firstElementChild);
              content.style.transition = 'none';
              content.style.transform = 'translateY(0)';
              requestAnimationFrame(() => {
                content.style.transition = ''; // Reset transition after rAF
                this.isScrolling = false;
              });
            }, 500); // 应与CSS过渡时间相匹配
          }
        }, 20); // 每隔2秒滚动一次
      }
    },
    mounted() {
      this.startScroll();
    },
    beforeDestroy() {
      clearInterval(this.scrollInterval); // 清除定时器以防内存泄漏
    }

  }
</script>

<style scoped>
  .scroll-container {
    height: 200px;
    /* 定义滚动容器的高度 */
    overflow: hidden;
    position: relative;
  }

  .scroll-content {
    list-style: none;
    margin: 0;
    padding: 0;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    transition: transform 0.5s linear;
  }
</style>