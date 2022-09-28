<template>
  <div>
      <a-card :vocabular=voc></a-card>
  </div>
  <button @click="clickedRandomVoc">Random Vocabular</button>
</template>

<script>
import ACard from '../components/ACard.vue'
export default {
  components:{
    ACard,
  },
  props:{
    myVocList:{
      required : true,
      type : Array
    }
  },
  data(){
        return{
            voc: '...',
        }
    },
  methods:{
    clickedRandomVoc(){
      this.voc = this.myVocList[Math.floor(Math.random() * this.myVocList.length)]
    }
  }
}
</script>

