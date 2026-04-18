<template>
   <div class="card p-4 mt-4 shadow text-center">
    <h3 class="mb-3">Current Weather</h3>

    <div class="row">
        <div class="col-md-6 mb-3">
            <div class="border rounded p-3">
                <h5><span class="badge bg-info text-dark">Temperature</span></h5>
                <h2>{{ weather.current.temperature_2m }}</h2>
            </div>
        </div>

        <div class="col-md-6 mb-3">
            <div class="border rounded p-3">
                <h5><span class="badge bg-warning text-white">Wind</span></h5>
                <h2>{{ weather.current.wind_speed_10m }}</h2>
            </div>
        </div>
    </div>
   </div> 
</template>
<script>
export default{
    props:["weather"]
}
</script>