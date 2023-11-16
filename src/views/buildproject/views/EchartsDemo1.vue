<template>
    <div>
        <div class="box" ref="boxRef"></div>
    </div>
</template>

<script>
import * as echart from 'echarts'
export default {
    mounted(){
        //配置选项
        let options={
            xAxis:{
                data:['成都','西安','天府']
            },
            yAxis:{},
            tooltip:{},
            legend:{},
            toolbox:{
                feature:{
                    saveAsImage:{},
                    restore:{},
                    dataView:{},
                    magicType:{
                        type:['line','bar']
                    },
                    dataZoom:{}
                }
            },
            series:[
                {
                    type:'bar',
                    name:'一月招生量',
                    data:[98,67,45]
                },
                {   type:'bar',
                    name:'二月招生量',                
                    data:[98,100,6]
                },
                {   type:'bar',
                    name:'三月招生量',
                    data:[62,11,6]
                },                                        
                {    
                
                    label:{
                        show:true
                    },
                    itemStyle:{
                        color:'orange',
                    },
                    barwidth:30,
                    markpoint:{
                        data:[
                            {
                                type:'max',name:'最大值'
                            }
                        ]
                    },
                    markline:{
                        data:[
                            {
                                type:'average',name:'平均值'
                            }
                        ]
                    }
                }
            ]
        }
        //初始化echarts
        let mychart=echart.init(this.$refs.boxRef)//mychart叫啥都行
        mychart.setOption(options)
    }
}
</script>

<style scoped lang="scss">
    .box{
        width: 500px;
        height: 500px;
        background-color:rgb(239, 242, 247);
    }
</style>