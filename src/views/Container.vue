<template id="container">
  <div class="content">
    <input type="text" v-if="input_flag" @keyup.enter="add" />
    <div class="card" v-for="(todo,index) in todos" :key="todo.id">
      <div class="card-content">
        <div class="card-content-inner">
          <p>{{ todo.task }}</p>
          <div class="btn-box pull-right">
            <button
              class="button button-success"
              :class="{'button-fill': todo.done }"
              @click="changeContainerFlag( index )"
            >
              <i class="icon icon-check"></i>
            </button>
            <button class="button button-danger" @click="checkDone( index )">
              <i class="icon icon-remove"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      input_flag: false
    };
  },
  props: ["todos", "change_mask_flag"],
  methods: {
    input_flag_change() {
      this.input_flag = !this.input_flag;
    },
    changeContainerFlag(index) {
      this.$emit("change_flag", index);
    },
    checkDone(index) {
      this.$emit("check", index);
    },
    add(e) {
      this.$emit("add_item", e.target.value);
      this.input_flag = false;
    }
  }
  // mounted() {
  //   var that = this;
  //   bus.$on("input_flag_change", function() {
  //     that.input_flag = !that.input_flag;
  //   });
  // }
};
</script>



<style lang="stylus" scoped>
.card-content-inner {
  overflow: hidden;

  .btn-box {
    display: flex;

    button {
      margin-right: 10px;
    }
  }
}
</style>