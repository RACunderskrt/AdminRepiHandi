<template>
    <div class="activitycomp" >
        <div class="data">
            <div class="title">
                <h2>{{ data.id }} - {{ data.name }}</h2>
                <div class="listBtn">
                    <div class="btn" @click="switchMore">Plus</div>
                    <!--div class="btn" @click="$emit('ban')" v-if="data.id_role != 3">Ban</div>
                    <div class="btn" @click="$emit('user')" v-else>DéAdmin</div-->
                </div>
            </div>
            <div class="tab" v-if="displayMore">
                <div> 
                    <h4>Description : {{ data.description }}</h4>
                </div>
                <div>
                    <h4>Id de l'aidant : {{ data.id_user }}</h4>
                </div>
                <div>
                    <h4> Date de début : {{ data.start }}</h4>
                </div>
                <div>
                    <h4> Date de fin : {{ data.end }}</h4>
                </div>
            </div> 
        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
    name: "ActivityComp",
    data(){
        return{
            displayMore: false
        }
    },
    props:{
        data: Object
    },
    mounted(){
        this.getStartdate();
        this.getEnddate();
        this.getName();
    },
    methods:{
        getStartdate(){
            let dada = new Date(this.data.start)
            dada = dada.toLocaleString('fr-FR', { timeZone: 'UTC' });
            this.data.start = dada
        },
        getEnddate(){
            let dada = new Date(this.data.end)
            dada = dada.toLocaleString('fr-FR', { timeZone: 'UTC' });
            this.data.end = dada
        },
        getName() {
            let initial = this.data.name.charAt(0).toLocaleUpperCase('fr-FR');
            let rest = this.data.name.slice(1).toLocaleLowerCase('fr-FR');
            this.data.name = initial + rest;
        },

        switchMore(){
            this.displayMore = !this.displayMore;
        },
    }
})
</script>
<style lang="scss" scoped>
.activitycomp{
    background-color:#88B2E3;
    margin:5px;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 5px 5px 2px 1px rgba(0, 0, 0, .05);
}
.title{
    display: grid;
    grid-template-columns: 70% auto;
}
.tab{
    display: grid;
    grid-template-columns: 25em auto;
    background: white;
    margin:5px;
    border-radius: 5px;
    padding: 20px;
}
.listBtn{
    display: grid;
    grid-template-columns: 120px 120px 120px;
}
.btn{
    position: relative;
    top:10px;
    width:75px;
    height: 20px;
    background: white;
    border-radius: 5px;
    border: solid black;
    margin:5px;
    padding:10px;
    text-align: center;
    font-weight: bold;
}


</style>