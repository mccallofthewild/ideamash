
<template lang="pug">
  textarea(rows="1", :placeholder="placeholder", :cols="cols", v-model="val", @keydown.enter="handleEnter")
</template>


<script>

  export default {
    props:{
      value:{
        default(){
          return ""
        }
      },
      class:{

      },
      placeholder:{

      }
    },
    data(){
      return {
        val:null
      }
    },
    methods:{
      handleEnter(e){
        e.preventDefault()
      }
    },
    computed:{
      cols(){
        let cols = 0;
        this.value.split('')
        .forEach(c=>{
          let lc = c.toLowerCase()

          let xl = /(m|w)/.test(lc);
          let sm = lc==c
          let xs = /(l|i|j|t|r)/.test(lc)
          let spc = /\s/.test(lc)

          let mod = 0;

          if(xl || !sm){
            mod = 1.8
          }else if(spc){
            mod = 0.6;
          }else if(sm){
            mod = 1.2;
          }else if(xs){
            mod = 1
          }
          cols += mod
        })
        return cols || 2
      },
    },
    mounted(){
      this.val = this.value
    },
    watch:{
      val(){
        this.$emit('input', this.val)
      },
      value(){
        this.val = this.value
      }
    }
  }

</script>


<style lang="scss" scoped>
   .input-container{
     display: inline-block;
     input{
     }
   }
</style>