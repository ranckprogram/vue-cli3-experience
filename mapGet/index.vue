<template>
  <div class="mpGet">
    <ul>
      <li
        v-for="recode in recodeList"
        :key="recode.id"
      >
        {{recode.proName}}
      </li>
    </ul>
  </div>
</template>

<script>

const api = {
  getProInfo() {
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve({
          id: "2",
          proName: Math.random()
        })
      }, 500)
    })

  }
}
export default {
  components: {},
  props: {},
  data() {
    return {
      recodeList: [{
        id: 2,
      },
      {
        id: 4,
      }]
    };
  },

  watch: {},
  created() {
    // 接在recodeList 获取成功的位置调用
    this.getProName()
  },
  mounted() { },
  methods: {
    getProName() {
      const result = []
      let count = -1;
      this.recodeList.forEach(async (item, index) => {
        const info = await api.getProInfo(item.id)
        count++
        result.push({
          ...item,
          proName: info.proName
        })
        item.proName = info.proName
        if (index === count) {
          this.recodeList = result
        }
      })
    }
  }
};
</script>

<style lang="less" scoped>
</style>