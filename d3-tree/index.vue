<template>
  <div class="tree">
    <div id="tree"></div>
  </div>
</template>

<script>
import * as d3 from 'd3'
export default {
  components: {},
  props: {},
  data() {
    return {
    };
  },
  computed: {},
  watch: {},
  created() { },
  mounted() {
    this.render()
  },
  methods: {

    render() {
      var data = {
        name: "china",
        children: [
          {
            name: "11",
            children: [
              {
                name: "11"
              },
              {
                name: "11"
              },
              {
                name: "11",
                children: [
                  {
                    name: "11"
                  },
                  {
                    name: "11"
                  },
                  {
                    name: "11"
                  },
                  {
                    name: "11"
                  },
                  {
                    name: "11"
                  },
                  {
                    name: "11"
                  },
                ]
              },
              {
                name: "11"
              },
              {
                name: "11"
              },
              {
                name: "11"
              },
            ]
          },
          {
            name: "11"
          },
          {
            name: "11"
          },
          {
            name: "11"
          },
          {
            name: "11"
          },
          {
            name: "11"
          },
        ]
      }

      var width = 960;
      var height = 500;

      const margin = { left: 100, top: 100, right: 50, bottom: 50 }

      var svg = d3.select("body").append("svg")
        .attr("width", width)
        .attr("height", height).call(d3.zoom().on("zoom", function () {
          svg.attr("transform", d3.event.transform)
        }))
        .append("g")

      var g = svg.append("g").attr('transform', 'translate(' + margin.left + ',' + margin.right + ')');

      var root = d3.hierarchy(data);
      console.log('root', root)

      console.log('后代', root.descendants())
      // Tree
      var tree = d3.tree()
        .size([width - margin.left - margin.right, height - margin.top - margin.bottom]);

      // Cluster	
      var cluster = d3.cluster()
        .size([height - margin.top - margin.bottom, width - margin.left - margin.right]);

      // Set initial vertical Tree
      var link = g.selectAll(".link")
        .data(tree(root).links())
        .enter().append("path")
        .attr("class", "link")
        .attr("fill", "none")
        .attr("stroke", "#ccc")
        .attr("d", d3.linkHorizontal()
          .x(function (d) { return d.y; })
          .y(function (d) { return d.x; }));

      var node = g.selectAll(".node")
        .data(root.descendants())
        .enter().append("g")
        .attr("class", function (d) { return "node" + (d.children ? " node--internal" : " node--leaf"); })
        .attr("transform", function (d) { return "translate(" + d.y + "," + d.x + ")"; })

      node.append("circle")
        .attr("r", 2.5);

      node.append("text")
        .text(function (d) { return d.data.name; })
        .attr('y', -10)
        .attr('x', -10)
        .attr('text-anchor', 'middle');

      node.on('click', function (node, number, element) {
        const selector = d3.select(this)
        handleClick(selector, { node, number, element })
      })

      // verticalCluster();
      // showcase();
      radialCluster();
      console.log(horizontalTree, radialTree, horizontalCluster, radialCluster, verticalCluster, verticalTree)


      function verticalTree() {
        // Transition to vertical
        /// 
        g.transition().attr("transform", 'translate(' + margin.left + ',' + margin.right + ')').duration(5000);
        tree.size([width - margin.left - margin.right, height - margin.top - margin.bottom]);
        link.data(tree(root).links())
          .transition()
          .attr("d", d3.linkVertical()
            .x(function (d) { return d.x; })
            .y(function (d) { return d.y; }))
          .duration(5000);

        node.transition()
          .attr("transform", function (d) { return "translate(" + d.x + "," + d.y + ")"; })
          .duration(5000)
      }



      function horizontalTree() {
        // Transition to horizontal
        /// 
        g.transition().attr("transform", 'translate(' + margin.left + ',' + margin.right + ')').duration(5000);
        tree.size([height - margin.top - margin.bottom, width - margin.left - margin.right]);
        link.data(tree(root).links())
          .transition()
          .attr("d", d3.linkHorizontal()
            .x(function (d) { return d.y; })
            .y(function (d) { return d.x; }))
          .duration(5000);

        node.transition()
          .attr("transform", function (d) { return "translate(" + d.y + "," + d.x + ")"; })
          .duration(5000);
      }

      function radialTree() {
        // Transition to Radial
        //
        g.transition().attr("transform", "translate(" + width / 2 + "," + height / 2 + ")").duration(5000);
        tree.size([2 * Math.PI, height / 2]);
        link.data(tree(root).links())
          .transition()
          .attr("d", d3.linkRadial()
            .angle(function (d) { return d.x; })
            .radius(function (d) { return d.y; }))
          .duration(5000);

        node.transition()
          .attr("transform", function (d) { return "translate(" + radialPoint(d.x, d.y) + ")"; })
          .duration(5000);

      }

      function horizontalCluster() {
        g.transition().attr("transform", 'translate(' + margin.left + ',' + margin.right + ')').duration(5000);
        cluster.size([height - margin.top - margin.bottom, width - margin.left - margin.right]);
        link
          .data(cluster(root).links())
          .transition()
          .attr("d", function (d) {
            console.log(d);
            return "M" + d.source.y + "," + d.source.x
              + "C" + (d.source.y + 100) + "," + d.source.x
              + " " + (d.source.y + 100) + "," + d.target.x
              + " " + d.target.y + "," + d.target.x;
          })
          .duration(5000)

        node.transition()
          .attr("transform", function (d) { return "translate(" + d.y + "," + d.x + ")"; })
          .duration(5000);
      }

      function verticalCluster() {
        g.transition().attr("transform", 'translate(' + margin.left + ',' + margin.right + ')').duration(5000);
        cluster.size([width - margin.left - margin.right, height - margin.top - margin.bottom]);
        link
          .data(cluster(root).links())
          .transition()
          .attr("d", function (d) {
            console.log(d);
            return "M" + d.source.x + "," + d.source.y
              + "C" + d.source.x + "," + (d.source.y + 60)
              + " " + d.target.x + "," + (d.source.y + 60)
              + " " + d.target.x + "," + d.target.y;
          })
          .duration(5000)

        node.transition()
          .attr("transform", function (d) { return "translate(" + d.x + "," + d.y + ")"; })
          .duration(5000);
      }

      function radialCluster() {
        g.transition().attr("transform", "translate(" + width / 2 + "," + height / 2 + ")").duration(5000);
        cluster.size([2 * Math.PI, height / 2 - 40]);

        link
          .data(cluster(root).links())
          .transition()
          .attr("d", function (d) {
            return "M" + radialPoint(d.source.x, d.source.y)
              + "C" + radialPoint(d.source.x, (d.target.y + d.source.y) / 2)
              + " " + radialPoint(d.target.x, (d.target.y + d.source.y) / 2)
              + " " + radialPoint(d.target.x, d.target.y);
          })
          .duration(5000)

        node.transition()
          .attr("transform", function (d) { return "translate(" + radialPoint(d.x, d.y) + ")"; })
          .duration(5000);
      }

      function radialPoint(x, y) {
        return [(y = +y) * Math.cos(x -= Math.PI / 2), y * Math.sin(x)];
      }

      console.log(horizontalTree, radialTree, horizontalCluster, radialCluster, verticalCluster, verticalTree)
      // var i = 1;

      // function showcase() {
      //   setTimeout(function () {
      //     if (++i % 6 == 4) { horizontalTree(); }
      //     else if (i % 6 == 2) { radialTree(); }
      //     else if (i % 6 == 5) { horizontalCluster(); }
      //     else if (i % 6 == 3) { radialCluster(); }
      //     else if (i % 6 == 1) { verticalCluster(); }
      //     else { verticalTree(); }
      //     showcase();
      //   }, 5500)



      // }


      function handleClick(selector, { node, element, number }) {

        console.log(node)
        console.log(element)
        console.log(number)
        console.log(selector)
        // selector.remove()
        console.log(node.data)
        // node.data.children = []
        console.log('list', selector.nodes())
      }
      console.log(d3.select("body").selectAll(".node")
      )
    }
  }
};
</script>

<style lang="less" scoped>
</style>