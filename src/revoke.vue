<template>
  <div class="red">
    <div>{{history}}</div>
    <button @click="fn1">+1</button>
    <button @click="fn2">+2</button>
    <button @click="fn11">-1</button>
    <button @click="fn22">-2</button>
    <div><button @click="che">回退</button>
      <button @click="che1">前进</button>
    </div>
    
  </div>
</template>





<script>

export default {
  data() {
    return {
      zzz: 1,
      n: 0,
      history: [],
      back:[],
      inUndoMode: false,
      backOn:false,
    }
  },
  watch: {
    n:function(nv,ov){
       this.zzz  = ov
       if(this.inUndoMode == false){
        this.history.push({from:ov,to:nv})
        console.log(this.zzz)
      }else if(this.inUndoMode == true){
        console.log('在true里')
      }
    }
  },
  methods: {
    fn1() {
      this.n  +=1
      this.delChe1()
    },
    fn2() {
      this.n  +=2
      this.delChe1()
    },
    fn11() {
      this.n  -=1
      this.delChe1()
    },
    fn22() {
      this.n  -=2
      this.delChe1()
    },
    che(){
        const numData=this.history.pop()
        this.back.push(numData)
        this.inUndoMode = true
        this.n = this.zzz    //watch是异步的，如果不做settimeout，
        //它会先把 inUndoMode 设为true 再设为false，再执行n的赋值，这样inUndoMode永远是false了
        //又因为这样n改变了，而inUndoMode 又一直是false，
        //表现在页面就是先删除旧的立刻补上了一个新的
        //且数据是运算后的
        //所以需要在watch的异步后再做一次异步，如果异步的优先级是同等的话，
        //就会先做完上一级的异步，再执行下一步的异步
        //这样就能保证在赋值给n时，inUndoMode是true了

        setTimeout(() => {   //这里vue 其实不是用settimeout，而是 $nextTick() 这是vue自己写的API
          this.inUndoMode = false  
        }, 0);
        

    },
    che1(){
      if(this.back.length >0 && this.backOn == false){
        const back=this.back.pop()
      this.history.push(back)
      }else{console.log('前进已完成')}
    },
    delChe1(){
      if(this.back.length !== 0){
      this.back = []
      console.log('因为回退后重新加入新的元素，回退前的元素已被删除')
      }
    }
  }

}
</script>





<style lang="scss">
.red {
  border: 1px solid red;
  color: red;
}
</style>
