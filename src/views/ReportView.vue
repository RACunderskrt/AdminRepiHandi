<template>
    <div class="page">
        <div class="title">
            <h1> Liste de tous les Signalements - {{ displayedData.length }} </h1>
        </div>
        <div 
            class="list" 
            v-for="d in displayedData" 
            v-bind:key="d.id"
        >
            <ReportComp 
                :data="d"
                @delete="deleteActivities(d)"
                @ignore="updateReport(d)"
                v-if="!d.done"
            />
        </div>
        <CheckComp 
            :textDialog="textModal"
            class="modal"
            :class="{active: displayModal}"
        />
    </div>
</template>

<script>
import { defineComponent } from 'vue'
import CheckComp from '@/components/CheckComp.vue';
import ReportComp from '@/components/ReportComp.vue';

export default defineComponent({
    name: "UserView",
    data(){
        return{
            data: [],
            displayedData: [],
            displayModal: false,
            textModal: ""
        } 
    },
    components:{
        CheckComp, ReportComp
    },
    mounted(){
        this.refreshData();
    },
    methods:{
        async refreshData(){
            this.data = []
            //let response = await fetch('https://sae-repihandi-api.onrender.com/user')
            let response = await fetch('http://localhost:4000/report')
            response = await response.json()
            this.data = response
            this.displayedData = this.data
            console.log(this.displayedData)
        },

        async updateUser(d,role){
            d.id_role = role
            console.log("user updated :",d)
            const sent = await fetch('http://localhost:4000/user', {
                method: 'POST',
                headers: {
                'Content-Type': 'application/json'
                },
                body: JSON.stringify(d)
            })
        },

        async updateReport(d){
            d.done = true
            console.log("report updated :",d)
            const sent = await fetch('http://localhost:4000/report/ignore/'+ d.id_activities, {
                method: 'POST'
            })
        },
        
        async deleteActivities(d){
            this.updateReport(d)
            const sent = await fetch('http://localhost:4000/activities/'+ d.id_activities, {
                method: 'DELETE'
            })
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