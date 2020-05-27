<template>
  <div >
    <div class = "calculator">
    <div class="display"> {{current || '0'}}</div>
    <div @click="clear()" class="resbtn">C</div>
    <div @click="sign()" class="resbtn">+/-</div>
    <div @click="percent()" class="resbtn">%</div>
    <div @click="divide()" class= "opbtn">÷</div>
    <div @click="append('7')" class="numbtn">7</div>
    <div @click="append('8')" class="numbtn">8</div>
    <div @click="append('9')" class="numbtn">9</div>
    <div @click="mul()" class= "opbtn">×</div>
    <div @click="append('4')" class="numbtn">4</div>
    <div @click="append('5')" class="numbtn">5</div>
    <div @click="append('6')" class="numbtn">6</div>
    <div @click="sub()" class= "opbtn">-</div>
    <div @click="append('1')" class="numbtn">1</div>
    <div @click="append('2')" class="numbtn">2</div>
    <div @click="append('3')" class="numbtn">3</div>
    <div @click="add()" class= "opbtn">+</div>

<div @click="append('0')" class="zero numbtn">0</div>
<div @click="Dot()" class="numbtn">.</div>

<div @click="equal()" class= "opbtn">=</div>

    </div>
  </div> 
</template>

<script>
export default {
  data()
  {
    return{
      prev:null,
      current: '555',
      operator: null,
      isCliscked:false,
    }
  },
  methods: {
    setPrev()
    {
        this.prev = this.current;
        this.isCliscked = true;
    },
    clear()
    {
       this.current = '';
    },
    sign()
    {
      if(this.current.length === 1 && this.current.charAt(0) === '0')
      {
        this.current = '0';
      }
      else
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent()
    {
      this.current = `${parseFloat(this.current)/100}`
    },
    append(number)
    {
      if(this.isCliscked === true)
      {
        this.current = '';
        this.isCliscked = false;
      }
      this.current = `${this.current}${number}`;
    },
    Dot()
    {
      if(this.current.indexOf('.') === -1)
      {
        this.append('.');
      }
    },
    divide()
    {
          this.operator = (a,b) => a/b;
          this.setPrev();
    },
    mul()
    {
         this.operator = (a,b) => a*b;
         this.setPrev();
    },
    add()
    {
         this.operator = (a,b) => a+b;
         this.setPrev();
    },
    sub()
    {
        this.operator = (a,b) => a-b;
        this.setPrev();
    },
    equal()
    {
      this.current = `${this.operator(parseFloat(this.current),parseFloat(this.prev))}`;
      this.prev=null;
    }

  }
  
}
</script>


<style scoped>
.calculator{
  width: 250px;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(55px, auto);
  font-size: 25px;
  margin: 0 auto;
 
}
.display{
  grid-column: 1/5;
  padding-top: 10px;
  background-color: rgb(53, 48, 58);
  color: white;
}
.zero{
  grid-column: 1/3;
}
.numbtn{
background-color:  #9c9a96;
border: 0.3px solid black;
color: white;
padding-top: 10px;

}
.opbtn{
 background-color: #ffbd00  ;
 border: 0.3px solid black;
color: white;
padding-top: 10px;

}
.resbtn{
background-color: #4e4c47  ;
 border: 0.3px solid black;
color: white;
padding-top: 10px;
}
</style>
