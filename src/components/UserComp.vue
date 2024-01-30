<template>
    <div class="usercomp"
    :class="{ ban: data.id_role == 3, admin: data.id_role == 1 }"
    >
        <div class="data">
            <div class="title">
                <h2>{{ data.id }} - {{ data.lastname }} {{ data.firstname }}</h2>
                <div class="listBtn">
                    <div class="btn" @click="switchMore">Plus</div>
                    <div class="btn" @click="$emit('ban')" v-if="data.id_role != 3">Ban</div>
                    <div class="btn" @click="$emit('user')" v-else>DéBan</div>
                    <div class="btn" @click="$emit('admin')" v-if="data.id_role != 1">Admin</div>
                    <div class="btn" @click="$emit('user')" v-else>DéAdmin</div>
                </div>
            </div>
            <div class="tab" v-if="displayMore">
                <div> 
                    <h4>Mail : {{ data.mail }}</h4>
                </div>
                <div>
                    <h4>Téléphone : {{ data.phone }}</h4>
                </div>
                <div>
                    <h4> Date de naissance : {{ data.birthdate }}</h4>
                </div>
                <div>
                    <h4> Adresse : {{ data.address }} - {{ data.postalcode }}</h4>
                </div>
            </div> 
        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
    name: "UserComp",
    data(){
        return{
            displayMore: false
        }
    },
    props:{
        data: Object
    },
    mounted(){
        this.getBirthdate();
        this.getFirstname();
        this.getLastname();
    },
    methods:{
        getBirthdate(){
            this.data.birthdate = this.data.birthdate.substring(0, 10)
        },
        getLastname(){
            //let prenom = new Date(this.data.end)
            this.data.lastname = this.data.lastname.toLocaleUpperCase('fr-FR');
            //this.data.end = dada
        },
        getFirstname() {
            let initial = this.data.firstname.charAt(0).toLocaleUpperCase('fr-FR');
            let rest = this.data.firstname.slice(1).toLocaleLowerCase('fr-FR');
            this.data.firstname = initial + rest;
        },

        switchMore(){
            this.displayMore = !this.displayMore;
        },
    }
})
</script>
<style lang="scss" scoped>
.usercomp{
    background-color:#88B2E3;
    margin:5px;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 5px 5px 2px 1px rgba(0, 0, 0, .05);
}
.ban{
    background-color:#e75959;
}
.admin{
    background-color: rgb(207, 205, 54);
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