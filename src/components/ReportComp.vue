<template>
    <div class="reportcomp" :class="{ ban: !data.done, validate: data.done }">
        <div class="data">
            <div class="title">
                <h2>{{ data.id }} - {{ data.name }} </h2>
                <h3>- Signalé par {{ data.lastname }} {{ data.firstname }}</h3>
                <div class="listBtn">
                    <div class="btn" @click="switchMore">Plus</div>
                    <div 
                        class="btn" 
                        @click="$emit('ignore')"
                        v-if="!data.done"
                    >
                        Ignorer
                    </div>
                    <div 
                        class="btn" 
                        @click="$emit('delete')"
                        v-if="!data.done"
                    >
                        Supprimer
                    </div>
                </div>
            </div>
            <div class="tab" v-if="displayMore">
                <div> 
                    <h4>Description : {{ data.description }}</h4>
                </div>
                <div>
                    <h4>Id de l'aidant : {{ data.id_user_reported }}</h4>
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
    name: "ReportComp",
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

        switchMore(){
            this.displayMore = !this.displayMore;
        },
    }
})
</script>
<style lang="scss" scoped>
.reportcomp{
    background-color:#88B2E3;
    margin:5px;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 5px 5px 2px 1px rgba(0, 0, 0, .05);
}
.title{
    display: grid;
    grid-template-columns: 40% 30% auto;
}
.ban{
    background-color:#e75959;
}
.validate{
    background-color: rgb(54, 207, 62);
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