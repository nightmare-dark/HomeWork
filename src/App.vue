<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <div class="page-group">
      <div class="page page-current">
        <!-- tab组件 -->
        <Tab :click="change_input_flag"></Tab>
        <!-- container组件 -->
        <Container
          ref="inp"
          :todos="newTodos"
          @change_flag="changeFlag"
          @add_item="addItem"
          @check="check"
        ></Container>
        <!-- mymask组件 -->
        <my-mask
          :remove="remove"
          :active_index="active_index"
          v-if="mask_flag"
          :close_mask="closeMask"
        ></my-mask>
        <!-- TabBar组件 -->
        <tab-bar :type="type" @get_type="changeType"></tab-bar>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import Tab from "./views/Tab";
import Container from "./views/Container";
import MyMask from "./views/MyMask";
import TabBar from "./views/TabBar";

export default {
  name: "app",
  data() {
    return {
      mask_flag: false,
      active_index: 0,
      type: "A",
      todos: [
        {
          id: 1,
          task: "任务一",
          done: true //done表示任务是否已经完成
        },
        {
          id: 2,
          task: "任务二",
          done: true
        }
      ]
    };
  },
  components: {
    // HelloWorld,
    Tab,
    Container,
    MyMask,
    TabBar
  },
  methods: {
    change_input_flag() {
      this.$refs.inp.input_flag_change();
    },
    changeFlag(index) {
      this.todos[index].done = !this.todos[index].done;
    },
    check(index) {
      /* index作用就是要让我们知道我们点的是哪一个 */
      const flag = this.todos[index].done;
      if (flag) {
        // true 那么表示任务已经完成，那么可以直接删除
        this.remove(index);
      } else {
        // false 那么表示任务没有完成，那么不可以直接删除，我们应该弹框提示
        this.active_index = index;
        this.changeMaskFlag();
      }
    },
    remove(index) {
      /* 数组删除一条 */
      this.todos.splice(index, 1);
    },
    changeMaskFlag() {
      /* 开启遮罩 */
      this.mask_flag = true;
    },
    closeMask() {
      this.mask_flag = false;
    },
    addItem(val) {
      /* 我们要往todos中添加一条 */
      this.todos.push({
        id: sort(this.todos)[0].id + 1,
        task: val,
        done: true
      });
    },
    changeType(val) {
      this.type = val;
    }
  },
  computed: {
    newTodos() {
      switch (this.type) {
        case "A":
          return this.todos;
          break;
        case "F":
          return this.todos.filter(item => item.done);
          break;
        case "U":
          return this.todos.filter(item => !item.done);
          break;

        default:
          break;
      }
    }
  }
};
function sort(arr) {
  return arr.sort(function(a, b) {
    return b.id - a.id;
  });
}
</script>

<style lang="stylus">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
