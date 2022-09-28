<template>
  <div class="grid-container">
    <div class="grid-item">
      <img :src="imageSrc" width="350">
    </div>
    <div class="grid-item">
      <div class="flex-container">
        <button id="btn1" @click="clickedButton1(selectedSigns[0])" :style="{background:buttonColor1}">{{selectedSigns[0]}}</button>
        <button id="btn2" @click="clickedButton2(selectedSigns[1])" :style="{background:buttonColor2}">{{selectedSigns[1]}}</button>
        <button id="btn3" @click="clickedButton3(selectedSigns[2])" :style="{background:buttonColor3}">{{selectedSigns[2]}}</button>
      </div>
    </div>
  </div>
  </template>

<script>

import a from '../assets/vowels/a.png'
import aa from '../assets/vowels/aa.png'
import aae from '../assets/vowels/aae.png'
import au from '../assets/vowels/au.png'
import e from '../assets/vowels/e.png'
import i from '../assets/vowels/i.png'
import ii from '../assets/vowels/ii.png'
import o from '../assets/vowels/o.png'
import r from '../assets/vowels/r.png'
import u from '../assets/vowels/u.png'
import uu from '../assets/vowels/uu.png'

import ba from '../assets/constants/ba.png'
import bha from '../assets/constants/bha.png'
import ca from '../assets/constants/ca.png'
import cha from '../assets/constants/cha.png'
import da from '../assets/constants/da.png'
import dda from '../assets/constants/dda.png'
import ddha from '../assets/constants/ddha.png'
import ga from '../assets/constants/ga.png'
import gha from '../assets/constants/gha.png'
import ja from '../assets/constants/ja.png'
import jha from '../assets/constants/jha.png'
import ka from '../assets/constants/ka.png'
import kha from '../assets/constants/kha.png'
import la from '../assets/constants/la.png'
import ma from '../assets/constants/ma.png'
import nga from '../assets/constants/nga.png'
import nna from '../assets/constants/nna.png'
import nya from '../assets/constants/nya.png'
import pa from '../assets/constants/pa.png'
import pha from '../assets/constants/pha.png'
import ra from '../assets/constants/ra.png'
import sha from '../assets/constants/sha.png'
import ssa from '../assets/constants/ssa.png'
import ta from '../assets/constants/ta.png'
import tha from '../assets/constants/tha.png'
import tta from '../assets/constants/tta.png'
import ttha from '../assets/constants/ttha.png'
import ya from '../assets/constants/ya.png'

export default {
  data(){
        return{
          imgListVowels : [a,aa,aae,au,e,i,ii,o,r,u,uu],
          imageSrc : null,
          imgListConstants : [ba,bha,ca,cha,da,dda,ddha,ga,gha,ja,jha,ka,kha,la,ma,nga,nna,nya,pa,pha,ra,sha,ssa,ta,tha,tta,ttha,ya],
          signListConstants : ["ba","bha","ca","cha","da","dda","ddha","ga","gha","ja","jha","ka","kha","la","ma","nga","nna","nya","pa","pha","ra","sha","ssa","ta","tha","tta","ttha","ya"],
          signListVowels : ["a","aa","aae","au","e","i","ii","o","r","u","uu"],
          currentImg : "",
          selectedSigns : [],
          buttonColor1 : 'grey',
          buttonColor2 : 'grey',
          buttonColor3 : 'grey'
        }
  },
  props:{
    onlyVowels:{
      required : true,
      type : Boolean
    }
  },
  mounted(){
    this.selectedSigns = this.randomList();
    this.chooseRandomImg();
  },
  methods:{
    chooseRandomImg(){
      //Activate all buttons
      this.activateAllBtns();

      let imgListLength = 0; 
      if(this.onlyVowels){
        imgListLength = this.imgListVowels.length
      }else{
        imgListLength = this.imgListConstants.length
      }
      const random = Math.floor(Math.random() * imgListLength);

      if(this.onlyVowels){
        this.imageSrc = this.imgListVowels[random]
        this.currentImg = this.signListVowels[random]
      }else{
        this.imageSrc = this.imgListConstants[random]
        this.currentImg = this.signListConstants[random]
      }

      this.buttonColor1 = 'grey',
      this.buttonColor2 = 'grey',
      this.buttonColor3 = 'grey',
      this.selectedSigns = this.randomList()
    },

    // Create a List with 3 random Sign (One of them being the real sign)
    randomList(){
        const correctButton = Math.floor(Math.random() * 3);
        const realSign = this.currentImg;
        // List without the correct Sign:
        let filteredSignList = [];
        if(this.onlyVowels){
          filteredSignList = this.signListVowels.filter(function(item){return item !== realSign})
        }else{
          filteredSignList = this.signListConstants.filter(function(item){return item !== realSign})
        }
        
        let x = null;
        let y = null;
        let z = null;

        let a = filteredSignList[Math.floor(Math.random() * filteredSignList.length)]
        let b = filteredSignList.filter(function(item){return item !== a})[Math.floor(Math.random() * (filteredSignList.length-1))]
        if(correctButton==1){
            x = this.currentImg
            y = a
            z = b
        }else if(correctButton==2){
            x = a
            y = this.currentImg
            z = b
        }else{
            x = a
            y = b
            z = this.currentImg
        }
        return [x,y,z]
    },
    clickedButton1(sign){
        if(sign==this.currentImg){
            this.buttonColor1 = 'green';
            this.deactivateAllBtns();
            setTimeout(() => {
              this.chooseRandomImg()
            }, "1000")
            
        }else{
            this.buttonColor1 = 'red';
            document.getElementById("btn1").disabled = true;
        }
    },
    clickedButton2(sign){
        if(sign==this.currentImg){
            this.buttonColor2 = 'green';
            this.deactivateAllBtns();
            setTimeout(() => {
              this.chooseRandomImg()
            }, "1000")
        }else{
            this.buttonColor2 = 'red';
            document.getElementById("btn2").disabled = true;
        }
    },
    clickedButton3(sign){
        if(sign==this.currentImg){
            this.buttonColor3 = 'green'
            this.deactivateAllBtns();
            setTimeout(() => {
              this.chooseRandomImg()
            }, "1000")
        }else{
            this.buttonColor3 = 'red';
            document.getElementById("btn3").disabled = true;
        }
    },
    deactivateAllBtns(){
      document.getElementById("btn1").disabled = true;
      document.getElementById("btn2").disabled = true;
      document.getElementById("btn3").disabled = true;
    },
    activateAllBtns(){
      document.getElementById("btn1").disabled = false;
      document.getElementById("btn2").disabled = false;
      document.getElementById("btn3").disabled = false;
    },
  }  
  }
</script>
<style>
  .flex-container {
    display: flex;
    flex-wrap: wrap;
  }
  
  .flex-container > button {
    width: 30%;
    margin: 1.33%;
    border-radius: 25px;
    border: 2px solid #030303fa;
    text-align: center;
    line-height: 75px;
    font-size: 30px;
  }

  .grid-container {
  display: grid;
  grid-template-rows: 80% 20%;
  padding: 0px;
  row-gap: 30%;
  
  /* background-color: #1a8214; */
  }

  .grid-item {
  /* background-color: rgba(81, 255, 0, 0.8);
  border: 1px solid rgba(197, 16, 220, 0.8); */
  }
  </style>
