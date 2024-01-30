<template>
    <div class="page">
        <div class="title">
            <h1> Liste de toutes les Activités - {{ displayedData.length }} </h1>
            <select v-model=filter @change="sortData">
                <option value=0>Trier par</option>
                <option value="id">ID</option>
                <option value="name">Nom</option>
                <option value="start">Date de Début</option>
            </select>
            <input 
                type="text"
                v-model=search 
                placeholder="Rechercher" 
                @input="filterData"
            />
        </div>
        <div 
            class="list" 
            v-for="d in displayedData" 
            v-bind:key="d.id"
        >
            <ActivityComp 
                :data="d"

            />
        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue'
import ActivityComp from '@/components/ActivitiesComp.vue';
export default defineComponent({
    name: "ActivitiesView",
    /*props: {
        data: Array
    },*/
    data(){
        return{
            data: [],
            displayedData: [],
            filter: 0,
            search: "",
            displayModal: false,
            textModal: ""
        }
    },
    components:{
        ActivityComp
    },
    mounted(){
        this.refreshData();
    },
    methods:{
        async refreshData(){
            this.data = []
            //let response = await fetch('https://sae-repihandi-api.onrender.com/activities')
            let response = await fetch('http://localhost:4000/activities')
            response = await response.json()
            this.data = response
            this.displayedData = this.data
            console.log("act : ",this.displayedData)
        },
        sortData(){
            console.log(this.filter)
            switch(this.filter){
                case "id":
                    this.displayedData2.sort((a, b) => a.id - b.id)
                    break;
                case "name":
                    this.displayedData2.sort(this.compareData)
                    break;
                case "start":
                    this.displayedData2.sort(this.compareData)
                    break;
                default:
                    break;
            }     
        },
        compareData(a, b){
            if(a[this.filter] < b[this.filter])
                return -1
            if(a[this.filter] > b[this.filter])
                return 1
            return 0
        }
    }
})
</script>
<style lang="scss" scoped>
@import "/src/style/style.css";
.title{
    display: grid;
    grid-template-columns: 45% auto auto;
    input {
        height:30px;
        position:relative;
        top:20px;
    }
    select{
        height:35px;
        position:relative;
        top:20px;
        margin-right: 5px;
    }
}
</style>