<template>
  <div id="app">
    <h2>Static template:</h2>
    <Button>Hello</Button>
    <Button type="primary">Hello</Button>

    <h2>Dynamically inserted:</h2>
    <div ref="container">
      <button @click="onClick">Click to insert MyButtons</button>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import MyButton from "./components/MyButton";

export default {
  name: "app",
  components: { MyButton },
  provide() {
    return {
      theme: this.theme
    };
  },
  methods: {
    onClick() {
      var ComponentClass = Vue.extend(MyButton);
      var instance = new ComponentClass({
        propsData: { type: "primary" },
        parent: this
      });
      instance.$slots.default = ["Klikni me!"];
      instance.$mount(); // pass nothing
      this.$refs.container.appendChild(instance.$el);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<style module="theme">
.primary {
  /* now everybody likes green ;) */
  background-color: red;
  /* and css-colors! */
  color: white;
}
</style>