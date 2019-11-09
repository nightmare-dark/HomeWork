<template id="tabbar">
  <footer>
    <ul>
      <li
        class="circle"
        v-for="tabbar in tabbars"
        :key="tabbar.id"
        :class="[tabbar.class,type == tabbar.text && 'circle-fill']"
        @click="changeType(tabbar.text)"
      >{{tabbar.text}}</li>
    </ul>
  </footer>
</template>


<script>
export default {
  props: ["type"],
  data() {
    return {
      tabbars: [
        {
          id: 1,
          text: "A",
          class: "circle-success"
        },
        {
          id: 2,
          text: "F",
          class: "circle-primary"
        },
        {
          id: 3,
          text: "U",
          class: "circle-danger"
        }
      ]
    };
  },
  methods: {
    changeType(val) {
      this.$emit("get_type", val);
    }
  }
};
</script>


<style lang="stylus" scoped>
* {
  margin: 0;
  padding: 0;
  list-style: none;
}

footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 80px;
  border-top: 1px solid #ccc;
}

ul {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.circle {
  width: 60px;
  height: 60px;
  color: #ccc;
  border: 1px solid #ccc;
  text-align: center;
  line-height: 60px;
  border-radius: 50%;

  &.circle-success {
    border-color: green;
    color: green;

    &.circle-fill {
      background: green;
      color: white;
    }
  }

  &.circle-primary {
    border-color: blue;
    color: blue;

    &.circle-fill {
      background: blue;
      color: white;
    }
  }

  &.circle-danger {
    border-color: red;
    color: red;

    &.circle-fill {
      background: red;
      color: white;
    }
  }
}
</style>