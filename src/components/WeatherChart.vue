<template>
    <div class="mt-4">
        <h4 class="mb-4">Temperature Chart</h4>
        <div class="card p-3"> <!--Without height card shrinks-->
            <div style="overflow-x: auto;">
            <canvas ref="chart"></canvas>
            </div>
        </div>
    </div>
</template>
<script>
import { Chart } from 'chart.js/auto';
export default{
    props:["hourly"],
    mounted(){
        this.createChart();
    },
    methods:{
        createChart(){
            const labels = this.hourly.map(item =>item.time.split('T')[1]);
            const temps = this.hourly.map(item => item.temp);

            new Chart(this.$refs.chart,{
                type:"line",
                data:{
                    labels: labels,
                    datasets:[
                        {
                            label: "Temperature (°C)",
                            data:temps,
                            borderWidth:2,
                            tension:0.4
                        }
                    ]
                },
                options:{
                    responsive:true,
                    maintainAspectRatio: false, //lets chart fill container height
                    scales:{
                        y:{
                            beginAtZero:false
                        }
                    }
                }
            })
        }
    }
}
</script>