<template>
    <div class="modal">
        <div class="data">
            <h2>{{ textDialog }}</h2>
            <div class="btnList">
                <div class="btn" @click="$emit('cancel')">Annuler</div>
                <div class="btn" @click="$emit('success')">Valider</div>
            </div> 
        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
    name: "CheckComp",
    data(){
        return{
            
        }
    },
    props:{
        textDialog: String
    },
    mounted(){
    },
    methods:{
    }
})
</script>
<style lang="scss" scoped>
.modal{
    z-index:100;
    background-color: #88B2E3;
    width:50%;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 5px 5px 2px 1px rgba(0, 0, 0, .05);
    border: solid black;
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
}

.btnList{
    display:grid;
    grid-template-columns: 8em auto;
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