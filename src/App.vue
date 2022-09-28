<template>
  <div class="navbar-container" style="margin:5%">
    <button @click="gotoHome">Home</button>
    <button @click="gotoVocabulary">Vokabeln</button>
    <button @click="gotoSignsVowels">Vokale</button>
    <button @click="gotoSignsConstants">Konsunanten</button>
  </div>
  <div v-if="page=='signsVowels'">
    <signs-page :onlyVowels="true"></signs-page>
  </div>
  <div v-else-if="page=='signsConstants'">
    <signs-page :onlyVowels="false"></signs-page>
  </div>
  <div v-else-if="page=='vocabulary'">
    <display-voc :myVocList=vocList></display-voc>
  </div>  
  <div v-else>
    <add-voc></add-voc>
  </div> 
</template>

<script>
import AddVoc from './pages/AddVoc'
import DisplayVoc from './pages/DisplayVoc'
import SignsPage from './pages/SignsPage'

export default {
  name: 'App',
  components: {
    DisplayVoc,
    AddVoc,
    SignsPage
  },
  data(){
    return{
      page : "signsVowels",
      vocList:[]
    }
  },
  methods:{
    gotoHome(){
        this.page = 'home';
    },
    gotoVocabulary(){
        this.page = 'vocabulary';
    },
    gotoSignsVowels(){
        this.page = 'signsVowels';
    },
    gotoSignsConstants(){
        this.page = 'signsConstants';
    },       

    addVocToList(payload){
      this.vocList.push(payload);
    }
  }
}
</script>

<style>
  .navbar-container {
    display: flex;
    flex-wrap: wrap;
  }
  
  .navbar-container > button {
    width: 23%;
    margin: 3px;
    padding: 0;
    border-radius: 25px;
    border: 2px solid #030303fa;
    text-align: center;
    line-height: 20px;
    font-size: 11px;
  }

</style>