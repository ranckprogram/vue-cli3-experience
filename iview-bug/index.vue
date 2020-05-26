<template>
  <div class="">
    <Input
      v-model="value"
      placeholder="Enter something..."
      style="width: 300px"
      @on-change="handleChange"
    />

  </div>
</template>

<script>
import Vue from "vue";
import 'view-design/dist/styles/iview.css';

import { Input } from 'view-design';
Vue.component('Input', Input);
export default {
  components: {},
  props: {},
  data() {
    return {
      value: ""
    };
  },
  computed: {},
  watch: {
    value(val) {
      console.log("watch", val)
    }
  },
  created() { },
  mounted() { },
  methods: {
    handleChange(event) {
      console.log("event start")
      console.log(event)
      console.log(event.data)
      console.log("event end")

    }
  }
};
</script>

<style lang="less" scoped>
</style>