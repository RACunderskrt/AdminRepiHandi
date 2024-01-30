<template>
  <div class="apped">
    <div class="header">
      <h1>RépiAdmin</h1>
      <button @click="changeView(1)">Users</button>
      <button @click="changeView(2)">Pac</button>
      <button @click="changeView(3)">Activities</button>
      <button @click="changeView(4)">Report</button>
    </div>
    <UserView v-if="view == 1"/>
    <PacView v-if="view == 2"/>
    <ActivitiesView v-if="view == 3"/>
    <ReportView v-if="view == 4"/>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import PacView from './PacView.vue';
import UserView from './UserView.vue';
import ActivitiesView from './ActivitiesView.vue';
import ReportView from './ReportView.vue';


export default defineComponent({
  name: "HomeView",
  components:{
    PacView, UserView, ActivitiesView, ReportView
  },
  data() {
    return{
      view: 1
    }
  },
  props: {
      data: Array
  },
  methods:{
    changeView(x){
      this.view = x
    }   
  }
})
</script>
<style lang="scss" scoped>
.header{
  display: flex;
  align-items: center;
  padding: 20px;
  background-color:#88B2E3;
  border-radius: 15px;
  box-shadow: 5px 5px 2px 1px rgba(0, 0, 0, .05);
  h1 {
    padding-right: 150px;
  }

  button {
    padding-right: 50px;
    font-size: 25px;
    border: none;
    background: #88B2E3;
  }
}
</style>