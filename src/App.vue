<template>
  <div id="app">
    <div ref="list" class="render-list" @scroll="onScroll">
      <div :style="{height: data.length * 30 + 'px'}" class="list-phantom"></div>
      <div class="list-content" ref="content">
        <div class="list-item" v-for="i in render_data" :key="i">{{ i }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    let data = [];
    let render_data = [];
    for (let i = 0; i < 1000000; i++) {
      data.push(i + 1);
    }
    render_data = data.slice(0, 15);
    return {
      data,
      render_data
    };
  },
  methods: {
    onScroll() {
      const scrollTop = this.$refs.list.scrollTop;
      this.render_data = this.data.slice(
        Math.floor(scrollTop / 30),
        Math.floor(scrollTop / 30) + 15
      );
      this.$refs.content.style.webkitTransform = `translate3d(0, ${scrollTop -
        (scrollTop % 30)}px, 0)`;
    }
  }
};
</script>

<style>
.render-list {
  height: 400px;
  overflow: auto;
  width: 100%;
  border-style: solid;
  border-color: black;
  position: relative;
}
.list-phantom {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
.list-item {
  height: 30px;
  padding: 5px;
  box-sizing: border-box;
}
.list-content {
  position: absolute;
  left: 0;
  right: 0;
}
</style>
