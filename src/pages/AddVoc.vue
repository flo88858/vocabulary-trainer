<template>
  <div>
    <form @submit.prevent action="clickedAddButton">
        <label for="vocIn">Enter a new vocabular</label>
        <input v-model="vocabular" type="text" name="vocIn">
        <button @click="clickedAddButton">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  data(){
        return{
          vocabular : "",
        }
    },
  methods:{
    clickedAddButton(){
      this.$emit("addVocabular",this.vocabular)
      this.vocabular = ""
    }
  }
}
</script>

