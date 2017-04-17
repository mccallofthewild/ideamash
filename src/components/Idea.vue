
<template lang="pug">
  .idea-container
    .idea
      a(:href="twitterIntent", target="_blank")
        img(:src="twitterLogo")
      p#idea
        span Build something that uses 
        span.data.tech {{tech}} 
        span to help 
        span.data.job  {{job}}
        span.space
        span.data.action  {{action}}
      button(@click="mixup", :style="btnstyle") Give Me an Idea!
</template>


<script>
  import { 
    jobs, 
    actions,
    tech,
  } from '@/data'
  import Vue from 'vue'
  import twitterLogo from '@/assets/twitter.svg'

  function randomItem(arr){
    let randomIndex = ~~(Math.random()*arr.length);
    return arr[randomIndex];
  }

  export default {
    data(){
      return {
        job:'',
        action:'',
        tech:'',
        defaultCols:4,
        btnstyle:{},
        twitterLogo,
        fullSentence:''
      }
    },
    methods:{
      mixup(){
        this.btnstyle = {
          transform:`scale(1.1)`
        }
        let t = setTimeout(()=>{
          this.btnstyle = {
            transform:`scale(1)`
          }
        }, 150)

        this.job = randomItem(jobs)
        this.tech = randomItem(tech)
        this.action = randomItem(actions)
      
      },
    },
    computed:{
      twitterIntent(){
        return `https://twitter.com/intent/tweet?text=${encodeURIComponent(this.fullSentence)}&url=${encodeURIComponent(window.location.href)}&via=mccallthetall`
      }
    },
    updated(){
      this.fullSentence = `"${document.getElementById('idea').innerText},"`
    },
    beforeMount(){
      this.mixup();
    }

  }

</script>


<style lang="scss">
@import '../assets/css/mediaqueries';

  $mainfont: 'Open Sans', sans-serif;
  $black:#0d1012;
  $white:#FAFAFA;

  .idea-container{
    display:flex;
    justify-content: center;
    align-items: center;
    width:66%;
    min-height:100%;
    @include mobile {
      width:90%;
    }
    // border:1px solid rgba(black, 0.8);
    font-family: 'Fanwood Text', serif;
    font-family: 'Open Sans', sans-serif;
    .idea{
      @include mobile {
        font-size: 3rem;
        line-height: 5rem;
        min-height:70%;
        justify-self:flex-start;
      }
      display: flex;
      justify-content: space-between;
      align-items:center;
      flex-direction: column;
      position:relative;
      font-size:2.5rem;
      line-height: 4rem;
      color:$black;
      
      a{
        align-self: flex-end;
        position: absolute;
        top:0;
        right:0;
        img{
          height:3rem;
          filter: drop-shadow( 0px 1px 1px rgba($black, 0.3) );
          transition:filter 500ms ease-out;
          will-change: filter;
        }
        &:hover{
          animation:tada 1s;
          animation-fill-mode:both;
          img{
            filter: drop-shadow( 0px 0px 0px rgba($black, 0.6) );
          }
        }
      }
      textarea{
        border:none;
        outline:none;
        resize:none;
        vertical-align: middle;
      }
      .data{
        appearance:none;
        outline:none;
        padding-bottom:5px;
        border-bottom:4px solid $black;
        color:#83d2ff;
        font-size:1em;
        font-family: $mainfont;
        box-shadow: 0px 5px 2px -5px rgba($black, 0.5);

        // border-color:pink;
        // border-bottom:10px solid;
      }
      .tech{
        // color:lightseagreen;
      }
      .job{
        // color:dodgerblue;
      }
      .space{
        display: inline-block;
        width:1rem;
      }
      .action{
        // color:red;
      }
      button{
        all:unset;
        background-color:$black;
        color:$white;
        padding:10px;
        font-size:1.5rem;
        text-align: center;
        border-radius:4px;
        box-shadow: 0px 2px 3px rgba($black, 0.6);
        @include mobile {
          border-radius: 15px;
          font-size:3rem;
          padding:2rem;
          box-shadow: 0px 5px 10px rgba($black, 0.6);
        }
        line-height: 1em;
        text-transform: uppercase;
        cursor:url(../assets/fingers-crossed-cursor.ico), default;
        transition:transform 100ms ease-out;
      }
    }
  }

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}

$scaleMax:1.1;
$scaleMin:.9;
@keyframes tada {
  from {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }

  10%, 20% {
    -webkit-transform: scale3d($scaleMin, $scaleMin, $scaleMin) rotate3d(0, 0, 1, -3deg);
    transform: scale3d($scaleMin, $scaleMin, $scaleMin) rotate3d(0, 0, 1, -3deg);
  }

  30%, 50%, 70%, 90% {
    -webkit-transform: scale3d($scaleMax, $scaleMax, $scaleMax) rotate3d(0, 0, 1, 3deg);
    transform: scale3d($scaleMax, $scaleMax, $scaleMax) rotate3d(0, 0, 1, 3deg);
  }

  40%, 60%, 80% {
    -webkit-transform: scale3d($scaleMax, $scaleMax, $scaleMax) rotate3d(0, 0, 1, -3deg);
    transform: scale3d($scaleMax, $scaleMax, $scaleMax) rotate3d(0, 0, 1, -3deg);
  }

  to {
    -webkit-transform: scale3d(1, 1, 1);
    transform: scale3d(1, 1, 1);
  }
}
</style>