<template>
  <div class="container">
    <div>第{{n}}手</div>
    <div class="row">
      <Cell :n="n" @click="cellClick(0,$event)" v-if="update"/>
      <Cell :n="n" @click="cellClick(1,$event)" v-if="update"/>
      <Cell :n="n" @click="cellClick(2,$event)" v-if="update"/>
    </div>
    <div class="row">
      <Cell :n="n" @click="cellClick(3,$event)" v-if="update"/>
      <Cell :n="n" @click="cellClick(4,$event)" v-if="update"/>
      <Cell :n="n" @click="cellClick(5,$event)" v-if="update"/>
    </div>
    <div class="row">
      <Cell :n="n" @click="cellClick(6,$event)" v-if="update"/>
      <Cell :n="n" @click="cellClick(7,$event)" v-if="update"/>
      <Cell :n="n" @click="cellClick(8,$event)" v-if="update"/>
    </div>
    <!-- <div>{{map}}</div> -->
    <div class="jieguo">结果：{{result===''? '输赢未定':`胜方为${result}`}}</div>
    <!-- <span class="btn" @click="reload">再来一局</span> -->
  </div>
</template>
<script>
import Cell from './Cell'
export default {
  components:{Cell},
  data(){
    return {
      n:0,
      result:'',
      update:true, //判断组件页面重新渲染与否
      isend: false,
      map:[[null,null,null],[null,null,null],[null,null,null]]
    }
  },
  methods: {
    cellClick(i,text){
      this.n += 1
      this.map[Math.floor(i/3)][i%3] = text
      this.win()
      this.isended()
    },
    win(){
      for(let i=0; i<3; i++){
        if(this.map[i][0]!==null && this.map[i][0]===this.map[i][1] && this.map[i][1]===this.map[i][2]){
          this.result = this.map[i][0]
        }
      }
      for(let j=0; j<3; j++){
        if(this.map[0][j]!==null && this.map[0][j]===this.map[1][j] && this.map[1][j]===this.map[2][j]){
          this.result = this.map[0][j]
        }
      }
      if(this.map[0][0]!==null && this.map[0][0]===this.map[1][1] && this.map[1][1]===this.map[2][2]){
          this.result = this.map[0][0]
        }
      if(this.map[0][2]!==null && this.map[0][2]===this.map[1][1] && this.map[1][1]===this.map[2][0]){
          this.result = this.map[0][2]
        }
      if(this.n === 9){
        this.isend = true
      }
    },
    isended(){
       if(this.isend ||this.result){
          let _this = this //setTimeout中的this指向window
          if(this.result===''){
            setTimeout(function(){
              alert('输赢未定,游戏结束')
              _this.reload()
              },0)
          }else{
            setTimeout(function(){
              alert(`胜方为${_this.result}，游戏结束`)
              _this.reload()
              console.log(_this.map)
              },0)
          }
        // this.reload()
        }

    },
    reload() {
    // 之前，忘记在组件Cell上使用v-if="update"，this.nextTick()死活不刷新，update的值控制组件是否重新渲染
     this.update = false
     this.n = 0
     this.result = ''
     this.isend = false
     this.map = [
        [null,null,null],
        [null,null,null],
        [null,null,null]
        ]
     this.$nextTick(() => (this.update = true))
    }
}
}
</script>
<style>
.container {
  width: 150px;
  margin: 0 auto;
  text-align: center
}
.row {
  display: flex;
}
.btn {
  box-sizing: border-box;
  display: inline-block;
  width: 150px;
  padding: 10px;
  background-color: aquamarine;
  border-radius: 10px;
  cursor: pointer;
}
.jieguo {
  margin: 10px;
}
</style>
