<template>
    <div class="mt-3">
        <h4 class="mb-3">Hourly Forecast</h4>
        <div class="d-flex overflow-auto">
            <div class="card p-3 text-center mr-4"
                 v-for="(item,index) in hourly"
                 :key="index"
                 style="min-width: 120px;">
                 <p>{{ formatTime(item.time) }}</p>
                 <h5>{{ item.temp }}</h5>
            </div>
        </div>
    </div>

</template>
<script>


export default{
    props:["hourly"],
    methods:{
        formatTime(time){
            return time.split('T')[1];   //split("T")[0]-"2026-04-18"  (date) split("T")[1]-"12:00" (time) 
        }
    }
}
</script>