<template>
  <div class="hello">
    <div id="container"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {

      var colors = {};
      var GDPSpeed = {
        // '520000':10,//贵州
        // '540000':10,//西藏
        // '530000':8.5,//云南 
        // '500000':8.5,//重庆
        // '360000':8.5,//江西
        // '340000':8.0,//安徽
        '510000': 7.5,//四川
        // '350000':8.5,//福建
        // '430000':8.0,//湖南
        // '420000':7.5, //湖北
        // '410000':7.5,//河南
        // '330000':7.0,//浙江
        // '640000':7.5,//宁夏
        // '650000':7.0,//新疆
        // '440000':7.0,//广东
        // '370000':7.0,//山东
        // '450000':7.3,//广西
        // '630000':7.0,//青海
        // '320000':7.0,//江苏
        // '140000':6.5,//山西
        // '460000':7,// 海南
        // '310000':6.5,//上海
        // '110000':6.5, // 北京
        // '130000':6.5, // 河北
        // '230000':6, // 黑龙江
        // '220000':6,// 吉林
        // '210000':6.5, //辽宁
        // '150000':6.5,//内蒙古
        // '120000':5,// 天津
        // '620000':6,// 甘肃
        // '610000':8.5,// 甘肃
        // '710000':2.64, //台湾
        // '810000':3.0, //香港
        // '820000':4.7 //澳门

      }
      var getColorByDGP = function (adcode) {
        if (!colors[adcode]) {
          var gdp = GDPSpeed[adcode];
          if (!gdp) {
            colors[adcode] = 'transparent'
          } else {
            var r = 3;
            var g = 140;
            var b = 230;
            var a = gdp / 10;
            colors[adcode] = 'rgba(' + r + ',' + g + ',' + b + ',' + a + ')';
          }
        }
        return colors[adcode]
      }
      var disCountry = new AMap.DistrictLayer.Country({
        zIndex: 13,
        SOC: 'CHN',
        depth: 1,
        styles: {
          'nation-stroke': '#fff',
          'coastline-stroke': 'fff',
          'province-stroke': 'white',
          'fill': function (props) {
            return getColorByDGP(props.adcode_pro)
          }
        }
      })

      var map = new AMap.Map("container", {
        zooms: [4, 10],
        center: [106.122082, 33.719192],
        zoom: 4,
        isHotspot: false,
        defaultCursor: 'pointer',
        layers: [
          disCountry
        ],
        viewMode: '2D',
        resizeEnable: true
      })

      var styleName = "amap://styles/" + "darkblue";
      map.setMapStyle(styleName);

      console.log(map)

    }


  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#container {
  width: 100%;
  height: 500px;
  opacity: .6;
}
.hello {
  background: url("./bg0.jpg");
}
</style>
