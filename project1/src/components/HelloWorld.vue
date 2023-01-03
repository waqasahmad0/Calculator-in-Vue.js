<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1> -->
    <div class="calculator">
      <div class="show">
        <p class="result">{{(current || 0)}}</p>
      </div>
      <div class=" buttons">
        <div class="row">
          <div class="col-md-3" @click="clear">AC</div>
          <div class="col-md-3" @click="sign">-/+</div>
          <div class="col-md-3 operator" @click="percent">%</div>
          <div class="col-md-3 operator" @click="divide">/</div>
        </div>
        <div class="row">
          <div class="col-md-3" @click="append('7')">7</div>
          <div class="col-md-3" @click="append('8')">8</div>
          <div class="col-md-3" @click="append('9')">9</div>
          <div class="col-md-3 operator" @click="times">x</div>
        </div>
        <div class="row">
          <div class="col-md-3" @click="append('4')">4</div>
          <div class="col-md-3" @click="append('5')">5</div>
          <div class="col-md-3" @click="append('6')">6</div>
          <div class="col-md-3 operator" @click="minus">-</div>
        </div>
        <div class="row">
          <div class="col-md-3" @click="append('1')">1</div>
          <div class="col-md-3" @click="append('2')">2</div>
          <div class="col-md-3" @click="append('3')">3</div>
          <div class="col-md-3 operator" @click="add">+</div>
        </div>
        <div class="row">
          <div class="col-md-3" @click="append('0')">0</div>
          <div class="col-md-3"> </div>
          <div class="col-md-3" @click="dot">.</div>
          <div class="col-md-3" @click="equal">=</div>
          <!-- <div class="col-md-3"></div> -->
        </div>
      </div>
    </div>
    <!-- <button @click="counter" class="btn btn-primary">Counter: {{count}}</button> -->
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      operatorClicked: false,
     current: '',
     previous: null,
     operator: null
    }
  },
  methods:{
      clear(){
        this.current=''
      },
      sign(){
        this.current=this.current.charAt(0)==='-'?this.current.slice(1): `-${this.current}`;
      },
      percent(){
        this.current=`${parseFloat(this.current)/100}`;
      },
      append(number){
        if(this.operatorClicked){
          // this.current= '';
          this.operatorClicked=false;
        }
        this.current=`${this.current}${number}`;
      },
      dot(){
        if(this.current.indexOf('.')=== -1){
          this.append('.');
        }
      },
      setPrevious(){
        this.previous=this.current;
        this.operatorClicked=true;
      },
      divide(){
        
        this.append('/');
        this.operator=(a,b)=>a/b;
        this.setPrevious();
      },
      times(){
        this.append('*');
        this.operator=(a,b)=>a*b;
        this.setPrevious();
      },
      add(){
        this.append('+');
        this.operator=(a,b)=>a+b;
        this.setPrevious();
      },
      minus(){
        this.operator=(a,b)=>a-b;
        this.setPrevious();
      },
      equal(){
        this.current=`${this.operator(
          parseFloat(this.current),
          parseFloat(this.previous)
        )}`;
        this.previous=null;
      }
    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .claculator{
    border: 1px solid black;
  }
  .show{
    margin: 0 auto;
    width: 40%;
    height: 100px;
    background-color: midnightblue;
  }
  .buttons{
    margin: 0 auto;
    width: 40%;
    background-color: slategray;
  }
  .col-md-3{
    width: 25%;
    border: 2px solid slategray;
    background-color: orange;
    padding-top: 20px;
    padding-bottom: 20px;
    cursor: pointer;

  }
  .col-md-6{
    border: 2px solid slategray;
    width: 50%;
    background-color: orange;
  }
  .row{
    display: flex;
  }
  .result{
    padding: 10px;
  }
  .result{
    color: white;
    font-size: 22px;
    float: left;
  }
</style>
