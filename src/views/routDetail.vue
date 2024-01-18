<template>
    <form v-if="rout!=null">
        <div class="row">
            <label>from</label>
            <input  v-model="fromcity">
        </div>
        <div class="row">
            <label>to</label>
            <input  v-model="tocity">
        </div>
        <div class="row">
            <label>cost</label>
            <input v-if="this.cost>10" v-model="this.cost" class="red-background">
            <input v-else v-model="this.cost">

        </div >
        <div class="row">
            <label>time</label>
            <input type="time" v-model="departuretime">
        </div>
        <div class="row">
            <label>date</label>
            <input type="date" v-model="departuredate">
        </div>
    </form>
    <button @click.prevent="updatePost(this.$route.params.id)">Update</button>
</template>

<script>
import Rout from './Rout.vue';

export default {
    data: function() {
        return {
            rout: null,
            fromcity:null,
            tocity:null,
            cost:null,
            departuretime:null,
            departuredate:null
        };
    },
    mounted() {
        this.fetchPost(this.$route.params.id);
    },
    components: {
        "rout-component": Rout
    },
    methods: {
        fetchPost(id) {
            fetch("http://localhost:3000/api/routes/" + id)
                .then((res) => res.json())
                .then((json) => {
                    this.rout = json[0];
                    this.fromcity = json[0].fromcity
                    this.tocity = json[0].tocity
                    this.cost = json[0].cost
                    this.departuretime = json[0].departuretime
                    this.departuredate = json[0].departuredate
                })
                .catch((err) => console.log(err));
        },
        updatePost(id){
            var payload ={
                fromcity:this.fromcity,
                tocity:this.tocity,
                cost:this.cost,
                departuretime:this.departuretime,
                departuredate:this.departuredate
            }
            console.log(payload)
            fetch("http://localhost:3000/api/routes/" + id, {
                method:"PUT",
                headers:{"Content-Type":"application/json"},
                credentials:"include",
                body:JSON.stringify(payload)
            }).then((res) => res.json()).then((json) => {
            }).catch((err) => console.log(err))
        }
    }
}
</script>

<style scoped>
    /* Add your styles here if needed */
    label{
        padding: 0.5em;
        height: fit-content;
        text-decoration: underline;
    }
    form{
        background-color: gray;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 0.5em;
        margin-left: 20%;
        margin-right: 20%;
        border-radius: 10px;
        padding: 0.75em;
    }
    .row{
        height: fit-content;
        width: 60%;
        margin: 0.25em;
        display: flex;
        flex-direction: column;
    }
    .red-background{
        background-color: red;
    }
    p{
        background-color: aliceblue;
        padding: 0.5em;
    }
</style>