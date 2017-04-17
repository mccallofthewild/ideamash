<template lang="pug">
  #app
    a.brand(:href="home")
      h1 Idea Mash
    .app-container
      Idea
    footer
      .credits-container
        .lg-credits
          p Built by 
            a(:href="mccallLink", target="_blank") McCall Alexander
            br
            .social
              a(href="https://www.instagram.com/mccallalexander/", target="_blank")
                img(:src="imgs.insta")
              a(href="https://github.com/mccallofthewild/", target="_blank")
                img(:src="imgs.gh")
              a(href="https://twitter.com/mccallthetall", target="_blank")
                img(:src="imgs.twitter")

        .sml-credits
          p Credits:
          span fingers crossed cursor:
            a(:href="stefanLink", target="_blank")  Stefan Wetterstrand;
          span twitter logo:
            a(:href="audreyLink", target="_blank") Andrey Vasiliev;
          span
            a(:href="nounProjLink", target="_blank") The Noun Project
</template>

<script>
import Idea from '@/components/Idea'
import twitter from '@/assets/twitter-logo.svg'
import insta from '@/assets/insta.svg'
import gh from '@/assets/github.svg'

function addRef(link){
  return `${link}/?ref=${encodeURIComponent(window.location.host)}`
}
export default {
  name: 'app',
  data(){
    return {
      imgs:{
        twitter,
        insta,
        gh,
      },
      mccallLink:addRef("https://mccallalexander.com"),
      stefanLink:addRef("http://steppot.com"),
      audreyLink:addRef("https://thenounproject.com/andvasiliev"),
      nounProjLink:addRef("https://thenounproject.com"),
      home:`${window.location.href}`
    }
  },
  components:{ Idea }
}

</script>

<style lang="scss">
@import './assets/css/mediaqueries';

$black:#171a1c;
// $black:#0d1012;
$white:#FAFAFA;

html{
  background:$black;
  @include md {
    font-size:16px;
  }
  @include mobile {
    font-size:30px;
  }
}


body{
  margin:0;
  background-color:$black;
  font-family:'Open Sans';
}
.brand{
  position: absolute;
  top:0;
  left:1rem;
  text-decoration: none;
  color:$black;
  h1{
    font-weight: normal;
  }
}
footer{
  display: flex;
  justify-content: center;
  align-items:center;
  flex-direction: column;
  background:$black;
  color:$white;
  width:100%;
}
.credits-container{
  display: flex;
  justify-content: space-around;
  align-items:center;
  @include mobile{
    flex-direction: column;
  }
  background:$black;
  width:90%;
  padding:5%;
  a{
    color:$white;
    // text-decoration: none;
  }
  .lg-credits{
    font-size: 2rem;
    .social{
      width:100%;
      display: flex;
      justify-content: space-between;
      img{
        max-height: 2.5rem;
      }
    }
  }
  .sml-credits{
    font-variant:small-caps;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: left;
  }
}
.app-container{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  min-height: 100%;
  min-height: 100vh;
  width:100vw;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color:#FAFAFA;
}

</style>
