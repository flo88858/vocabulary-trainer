<template>
<button @click="clickedButton1(randomSignList[0])" :style="{background:buttonColor1}">{{randomSignList[0]}}</button>
<button @click="clickedButton2(randomSignList[1])" :style="{background:buttonColor2}">{{randomSignList[1]}}</button>
<button @click="clickedButton3(randomSignList[2])" :style="{background:buttonColor3}">{{randomSignList[2]}}</button>
</template>

<script>
export default {
    data() {
        return {
            signList:["a","aa","aae","au","ii","o","u","uu"],
            randomSignList : [],
            buttonColor1 : 'grey',
            buttonColor2 : 'grey',
            buttonColor3 : 'grey'
        }
    },
    mounted(){
        this.randomSignList = this.randomList()
    },
    props:{
        actualSign:{
            type: String,
            required: true,
        }
    },
    computed:{

    },
    methods:{
        // Create a List with 3 random Sign (One of them being the real sign)
        randomList(){
            const correctButton = Math.floor(Math.random() * 3);
            const realSign = this.actualSign;
            // List without the correct Sign:
            const filteredSignList = this.signList.filter(function(item){return item !== realSign})

            let x = null;
            let y = null;
            let z = null;

            if(correctButton==1){
                x = this.actualSign
                y = filteredSignList[Math.floor(Math.random() * filteredSignList.length)]
                z = filteredSignList[Math.floor(Math.random() * filteredSignList.length)]
            }
            else if(correctButton==2){
                x = filteredSignList[Math.floor(Math.random() * filteredSignList.length)]
                y = this.actualSign
                z = filteredSignList[Math.floor(Math.random() * filteredSignList.length)]
            }else{
                x = filteredSignList[Math.floor(Math.random() * filteredSignList.length)]
                y = filteredSignList[Math.floor(Math.random() * filteredSignList.length)]
                z = this.actualSign
            }
            return [x,y,z]
        },
        clickedButton1(sign){
            if(sign==this.actualSign){
                this.buttonColor1 = 'green';
                
            }else{
                this.buttonColor1 = 'red';
            }
        },
        clickedButton2(sign){
            if(sign==this.actualSign){
                this.buttonColor2 = 'green';
            }else{
                this.buttonColor2 = 'red';
            }
        },
        clickedButton3(sign){
            if(sign==this.actualSign){
                this.buttonColor3 = 'green';
            }else{
                this.buttonColor3 = 'red';
            }
        }

    }
}
</script>
