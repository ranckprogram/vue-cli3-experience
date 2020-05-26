<template>
  <div
    class="pdf"
    id="pdf"
  >

    <table
      id="table"
      class="table"
      ref="table"
    >
      <tr>
        <th>姓名</th>
        <th>年龄</th>
      </tr>

      <tr>
        <td>ranck</td>
        <td>27</td>
      </tr>
      <tr>
        <td>ranck</td>
        <td>27</td>
      </tr>
      <tr>
        <td>ranck</td>
        <td>27</td>
      </tr>
      <tr>
        <td>ranck</td>
        <td>27</td>
      </tr>
      <tr>
        <td>ranck</td>
        <td>27</td>
      </tr>
    </table>
    <img
      class="pic"
      src="./pic.jpg"
      alt=""
    >

    <section class="paper">
      <p>1.愿所得皆所期，所失皆无碍</p>
      <p>2.最好的状态是未来可期</p>

      <p> 3.那些将要去的地方，都是素未谋面的故乡
      </p>

      <p> 4.对待自己温柔一点。你只不过是宇宙的孩子，与植物、星辰没什么两样。
      </p>
      <p> 5.热爱可抵岁月漫长。
      </p>
      <p> 6.我们各自努力，最高处见。
      </p>
    </section>
  </div>
</template>

<script>
import html2pdf from "html2pdf.js"

export default {
  components: {},
  props: {},
  data() {
    return {
    };
  },
  computed: {},
  created() {

  },
  mounted() {
    // const table =  this.$refs.table;
    const element = document.querySelector('#pdf')
    html2pdf(element);


  },
  methods: {},
  watch: {},
};
</script>

<style scoped>
.pdf {
  padding: 60px 40px;
}
.table {
  border: 1px solid #ddd;
  width: 100%;
  border-spacing: 0;
  border-collapse: collapse;
}

.table td,
.table th {
  padding: 4px 12px;
  border: 1px solid #ddd;
}

.pic {
  display: block;
  width: 300px;
  margin: 20px auto;
}

.paper {
  font-size: 16px;
  color: #333;
  line-height: 24px;
}
p {
  margin: 0 0 10px;
}
</style>