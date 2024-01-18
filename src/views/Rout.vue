<template>

<RouterLink :to="{name:'routDetail', params:{id:this.id}}">
    <div class="rout-row">
        <p>{{ from }}</p>
        <p> {{ to }}</p>
        <p>{{ cost }}</p>
        <p>{{ time }}</p>
        <p>{{ date }}</p>
    </div>    
</RouterLink>




</template>

<script>

export default{
    data() {
        return
    },
    props:{
        from:String,
        to:String,
        cost:String,
        time:String,
        date:String,
        id:String,
    },

}
</script>

<style scoped>
.rout-row{
    display: flex;
    justify-content:center;
    background-color: gray;
    border-radius: 20px;
    margin: 0.25em;
    
}
p{
    background-color: rgb(162, 132, 190);
    padding: 0.75em;
    width: 20%;
}
</style>