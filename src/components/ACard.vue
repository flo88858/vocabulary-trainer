<template>
  <div>
      Your vocabular: {{vocabular}}
  </div>
</template>

<script>
export default {
    data(){
        return{
            list:null,
        }
    },
    props:{
        vocabular:{
            type: String,
            required: true,
        }
    },
}
</script>
