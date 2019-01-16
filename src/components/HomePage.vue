<template>
  <div class="calculator">
    <div class="history"></div>
      <div class="screen">
        <span class="last">{{ calExpression }}</span>
        <span class="total">{{ total }}</span>
      </div>
      <div class="keys-btn">
        <div class="clearfix">
          <button class="calc_his imp" value="H">HIS</button>
          <button class="calc_cls imp" value="&#x21bb;" >&#x21bb;</button>
          <button class="calc_op imp"></button>
          <button class="calc_bac imp" value="&larr;" @click="onClickDelete()">&larr;</button>
        </div>
        <div class="clearfix">
          <button class="calc_cls imp" value="C" @click="onClickCalculateInt('C')">C</button>
          <button class="calc_his imp" value="H" @click="onClickCalculateInt('()')">()</button>
          <button class="calc_bac imp" value="%" @click="onClickCalculateInt('%')">%</button>
          <button class="calc_op imp" value="/" @click="onClickCalculateInt('/')">&divide;</button>
        </div>
        <div class="clearfix">
          <button class="calc_int" value="7" @click="onClickCalculateInt(7)">7</button>
          <button class="calc_int" value="8" @click="onClickCalculateInt(8)">8</button>
          <button class="calc_int" value="9" @click="onClickCalculateInt(9)">9</button>
          <button class="calc_op imp" value="*" @click="onClickCalculateInt('*')">&times;</button>
        </div>
        <div class="clearfix">
          <button class="calc_int" value="4" @click="onClickCalculateInt(4)">4</button>
          <button class="calc_int" value="5" @click="onClickCalculateInt(5)">5</button>
          <button class="calc_int" value="6" @click="onClickCalculateInt(6)">6</button>
          <button class="calc_op imp" value="-" @click="onClickCalculateInt('-')">-</button>
        </div>
        <div class="clearfix">
          <button class="calc_int" value="1" @click="onClickCalculateInt(1)">1</button>
          <button class="calc_int" value="2" @click="onClickCalculateInt(2)">2</button>
          <button class="calc_int" value="3" @click="onClickCalculateInt(3)">3</button>
          <button class="calc_op imp" value="+" @click="onClickCalculateInt('+')">+</button>
        </div>
        <div class="clearfix">
          <button class="calc_dec" value="." @click="onClickCalculateInt('.')">.</button>
          <button class="calc_int" value="0" @click="onClickCalculateInt(0)">0</button>
          <button class="calc_neg" value="-/+" @click="onClickCalculateInt('&plusmn;')">+/-</button>
          <button class="calc_eval" value="=" @click="onClickCalculateInt('=')">=</button>
        </div>
      </div>
    <ul style="display:none" class="history-list"></ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      total: 0,
      isAnInt: false,
      isAnOperator: false,
      prevValue: 0,
      prevOperator: '',
      calExpression: ''
    }
  },
  methods: {
    onClickCalculateInt(value) {
      if (value !== '=') {
        this.calExpression = this.calExpression.concat(value);
      }

      if (Number.isInteger(value)) {
        if (this.isAnOperator) {
          this.total = this.prevValue;
          this.prevValue = value;
          this.isAnOperator = false;
        } else {
          this.prevValue = parseInt('' + this.prevValue + value);
        }
      } else {
        if (value === '=') {
          if (this.prevOperator === '+') {
            this.total += this.prevValue;
          } else if (this.prevOperator === '-') {
            this.total -= this.prevValue;
          } else if (this.prevOperator === '*') {
            this.total *= this.prevValue;
          } else if (this.prevOperator === '%') {
            this.total %= this.prevValue;
          }

          this.calExpression = '';
          this.prevValue = 0;
        } else {
          this.isAnOperator = true;
          this.prevOperator = value;
        }
      }
    },
    checkAndDisplayAfterIsOperator(op, value) {

    },
    onClickDelete() {
      console.log('Delete');
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap.min.css');
.calculator{
	height:auto;
	padding:15px;
	font-size:1.3em;
	width:300px;
	/* background:#222; */
	box-shadow:0 10px 15px rgba(0,0,0,.2);
}
.calculator .screen{
	height:100px;
  color: #000;
	font-weight:bold;
	text-align:right;
	border-radius:3px;
	margin-bottom:7px;
	position:relative;
	/* background:rgba(0,0,0,.2); */
}
.calculator .screen .last,
.calculator .screen .total{
	color:#000;
	display:block;
	position:absolute;
}
.calculator .screen .last{
	top:3px;
	right:5px;
	font-size:1.4em;
	/* font-style:italic; */
	font-weight:normal;
}
.calculator .screen .total{
	bottom:0;
	right:5px;
	font-size:1.2em;
	width:100%;
	overflow:hidden;
  color: #999 !important;
	text-overflow:ellipsis;
}
.calculator .keys-btn button{
	top:0;
	float:left;
	color:#111;
	height:40px;
	border: .5px solid #000;
	width:24.5%;
	cursor:pointer;
	line-height:36px;
	user-select:none;
	position:relative;
	text-align:center;
	/* background:#d8d9db; */
	/* margin:0 .4% .4% 0; */
	/* background:linear-gradient(#d8d9db,#cecfd2); */
}
.calculator .keys-btn .calc_bac{
	font-size:22px;
	font-family:Consolas,"courier new";
}
.calculator .keys-btn .clearfix button:last-child{
	margin-right:0;
}
.calculator .keys-btn .exponent{
	top:-15%;
	font-size:.6em;
	text-indent:2px;
	position:absolute;
	font-weight:normal;
}
.calculator .keys-btn .denominator{
	position:relative;
}
.calculator button .denominator .denom-top,
.calculator .total .denominator .denom-top{
	left:-8px;
	top:-12px;
	font-size:.9em;
	position:absolute;
}
.calculator button .denominator .denom-slash,
.calculator .total .denominator .denom-slash{
	padding:0 1px;
	font-weight:normal;
}
.calculator button .denominator .denom-btm,
.calculator .total .denominator .denom-btm{
	top:-5px;
	font-size:.9em;
	position:absolute;
}

.calculator .keys-btn .imp{
	color: #148cd8;
	background:#d8d9db;
	/* background:linear-gradient(#f89112,#f78b11); */
}

.calculator .keys-btn button:hover, .calculator .keys-btn button.active{
	color:#222;
	background:white;
}
.calc_eval {
  color: #fff !important;
  background: green !important;
}
</style>
