<template>
  <div class="">{{message.message}}</div>
</template>

<script>
export default {
  components: {},
  props: {
    message: {
      type: Object,
      default: () => ({})
    }
  },
  data() {
    return {
    };
  },
  computed: {},
  watch: {},
  created() {
    console.log("child create")
  },
  mounted() {
    console.log("child mounted")
  },
  methods: {}
};
</script>

<style lang="less" scoped>
</style>