<template>
  <div class="cell" @click="change">
    <template v-if="a">{{text}}</template>
    <template v-else></template>
  </div>
</template>

<script>
export default {
  props:['n','result'],
  data(){
    return {
      a: false,
      text:''
    }
  },
  methods:{
    change(){
      // if(this.result) return 
      if(this.text !== '') return //点击过的格子不能再点击
      this.a = true
    //   console.log(this.n)
      this.text = this.n % 2 === 0? 'x':'o'
      this.$emit('click',this.text)
    }
  }
}
</script>
<style>
.cell {
  width: 50px;
  height: 50px;
  font-size: 40px;
  color: red;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  justify-items: center;
}
</style>
