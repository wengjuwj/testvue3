<template>
  <div class="hello">
    <div id="chinaEcharts" ref="chinaEcharts"   class="leftEcharts" style="height:400px;"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts'
import 'echarts/map/js/china.js'  //如果是npm下载的直接引入包里面的就可以，另外h5可以直接下载下来引入
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      data:[
          {name:"南海诸岛",value:0, count: 30},
          {name: '北京', value: 3, count: 30},
          {name: '天津', value: 5},
          {name: '上海', value: 6},
          {name: '重庆', value: 15},
          {name: '河北', value: 15},
          {name: '河南', value: 15},
          {name: '云南', value: 15},
          {name: '辽宁', value: 7},
          {name: '黑龙江', value: 5},
          {name: '湖南', value: 68},
          {name: '安徽', value: 34},
          {name: '山东', value: 34},
          {name: '新疆', value: 34},
          {name: '江苏', value: 34},
          {name: '浙江', value: 34},
          {name: '江西', value: 34},
          {name: '湖北', value: 34},
          {name: '广西', value: 34},
          {name: '甘肃', value: 34},
          {name: '山西', value: 34},
          {name: '内蒙古', value: 9},
          {name: '陕西', value: 16},
          {name: '吉林', value: 16},
          {name: '福建', value: 16},
          {name: '贵州', value: 16},
          {name: '广东', value: 43},
          {name: '青海', value: 43},
          {name: '西藏', value: 43},
          {name: '四川', value: 43},
          {name: '宁夏', value: 43},
          {name: '海南', value: 75},
          {name: '台湾', value: 75},
          {name: '香港', value: 75},
          {name: '澳门', value: 75}
        ]
    }
  },
  mounted(){
    this.chinaEcharts(this.data,99)
  },
  methods:{
    //    热力图
    chinaEcharts(dataList,maxNum) {
      // let this_ = this;
      let myChart = echarts.init(document.getElementById('chinaEcharts'));
      let resizeTimer = null;
      let option = {
            tooltip: {
                    formatter:function(params){
                        return params.seriesName+'<br />'+params.name+'：'+params.value
                    }//数据格式化
                },
            visualMap: {
                min: 0,
                max: maxNum,
                left: 'left',
                top: 'bottom',
                text: ['高','低'],//取值范围的文字
                inRange: {
                    color: ['#e0ffff', '#006edd']//取值范围的颜色
                },
                show:true//图注
            },
            geo: {
                map: 'china',
                roam: false,//不开启缩放和平移
                zoom:1.23,//视角缩放比例
                label: {
                    normal: {
                        show: true,
                        fontSize:'10',
                        color: 'rgba(0,0,0,0.7)'
                    }
                },
                itemStyle: {
                    normal:{
                        borderColor: 'rgba(0, 0, 0, 0.2)'
                    },
                    emphasis:{
                        areaColor: '#F3B329',//鼠标选择区域颜色
                        shadowOffsetX: 0,
                        shadowOffsetY: 0,
                        shadowBlur: 20,
                        borderWidth: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                    }
                }
            },
            series : [
                {
                    name: '信息量',
                    type: 'map',
                    geoIndex: 0,
                    data:dataList
                }
            ]
        };
      myChart.setOption(option);
    
      window.addEventListener('resize', function () {
        if (resizeTimer) clearTimeout(resizeTimer);
        resizeTimer = setTimeout(function () {
          myChart.resize();
        }, 100)
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
