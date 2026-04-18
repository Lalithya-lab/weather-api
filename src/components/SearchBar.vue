<template>
    <div class="input-group">
        <input v-model="city"
               type="text"
               placeholder="Enter city..."
               class="form-control">
        <button class="btn btn-primary" @click="search">Search</button>
    </div>
</template>
<script>


export default{
    data(){
        return{
            city:"",
        }
    },
    methods:{
        search(){
            this.$emit('search',this.city);
        }
    }
}
</script>
