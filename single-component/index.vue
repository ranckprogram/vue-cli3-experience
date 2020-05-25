<template>
  <div class="">
    hhh

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
  </div>
</template>

<script>
import jsPDF from "jspdf";

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
    const source = document.querySelector('#table')
    var pdf = new jsPDF();

    // console.log(doc)
    // doc.setTextColor(100);
    // doc.text(20, 20, 'This is gray.');
    // doc.setTextColor(150);
    // doc.text(20, 30, 'This is light gray.');
    // doc.setTextColor(255, 0, 0);
    // doc.text(20, 40, 'This is red.');
    // doc.setTextColor(0, 255, 0);
    // doc.text(20, 50, 'This is green.');
    // doc.setTextColor(0, 0, 255);
    // doc.text(20, 60, 'This is blue.');
    // doc.addHTML(table)

    // console.log(doc)
    // doc.save('two-by-four.pdf')
    const margins = {
      top: 80,
      bottom: 60,
      left: 40,
      width: 10000
    };

    const specialElementHandlers = {
      // element with id of "bypass" - jQuery style selector
      '#table': function (element, renderer) {
        // true = "handled elsewhere, bypass text extraction"
        console.log(element, renderer)
        return true
      }
    };

    pdf.fromHTML(
      source, // HTML string or DOM elem ref.
      margins.left, // x coord
      margins.top, { // y coord
      'width': margins.width, // max width of content on PDF
      'elementHandlers': specialElementHandlers
    },

      function (dispose) {
        // dispose: object with X, Y of the last line add to the PDF 
        //          this allow the insertion of new lines after html
        console.log(dispose)
        pdf.save('Test.pdf');
      }, margins);


  },
  methods: {},
  watch: {},
};
</script>

<style scoped>
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
</style>