<template>
    <div id="app">
        <div>
            <el-alert title="类似js-echarts原始图形配置, 数据来源: axios 返回 json对象" type="success">
            </el-alert>
        </div>
        <br>
        <hr>
        <div id="bar-chart" style="height: 400px; width: 100%;"></div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        this.myChart = null;
        this.option = {
            title: {
                text: 'Bar Demo 1'
            },
            tooltip: {
                trigger: 'axis'
            },
            legend: {
                textstyle:{
                    fontstyle:'italic',
                    color:'red'
                }
                //data: ['score of math']
            },
            xAxis: {
                data: [],
                type: 'category'
                // data:[1, 2, 3, 4, 5]
            },
            yAxis: {

            },
            series: [
                {
                    name: 'Score of Math',
                    type: 'bar',
                    data: []
                    // data:[2, 3, 5, 4, 6]
                }
            ]
        }
        return {

        }
    },
    created() {
        axios.get("/json/Score.json").then((result) => {
            let data = result.data;
            let datax = data.map((item) => { return item.name });
            let datay = data.map((item) => { return item.score });
            this.reSetOption(datax, datay);
        });
    },
    mounted() {
        this.myChart = this.$echarts.init(document.getElementById('bar-chart'))
        // console.log(this.option);
        this.myChart.setOption(this.option);
        window.myChart = this.myChart;
        window.onresize = function(){
            this.myChart.resize();
        }
    },
    methods: {
        reSetOption(datax, datay) {
            this.option.xAxis.data = datax;
            this.option.series[0].data = datay;
            this.myChart.setOption(this.option)
        }
    }
}
</script>

<style></style>