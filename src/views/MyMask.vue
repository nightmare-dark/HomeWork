<template id="mask">
  <div class="mask-box">
    <div class="bg" @click.self="close_mask"></div>
    <div class="mask-content">
      <p>您真的确定要删除我吗？</p>
      <button class="button button-primary button-fill pull-right" @click.self="confirm">确定</button>
    </div>
  </div>
</template>


<script>
export default {
  props: ["close_mask", "active_index", "remove"],
  methods: {
    confirm() {
      this.close_mask();
      this.remove(this.active_index);
    }
  }
};
</script>


<style lang="stylus" scoped>
.mask-box {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 10000;
  width: 100%;
  height: 100%;

  .bg {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: black;
    opacity: 0.5;
  }
}

.mask-content {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  width: 80%;
  height: 110px;
  background: white;
  border-radius: 10px;
  padding: 10px;
  overflow: hidden;

  button {
    width: 80px;
    height: 30px;
    font-size: 14px;
  }

  p {
    font-weight: bold;
  }
}
</style>