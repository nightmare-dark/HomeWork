<template id="tab">
  <header class="bar bar-nav">
    <a class="icon icon-left pull-left"></a>
    <i class="icon icon-edit pull-right" @click="hit"></i>
    <h1 class="title">666</h1>
  </header>
</template>


<script>
export default {
  props: ["click"],
  methods: {
    // change_input_flag() {
    //   bus.$emit("input_flag_change");
    // }
    hit() {
      this.click();
    }
  }
};
</script>


