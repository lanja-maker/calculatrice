<template>
  <div class="calculator">
    <div class="display">
      
      <form @submit.prevent="calculate">
        <div class="result">{{ result }}</div>
        <input type="text" v-model="inputStr" />
        <button type="submit">=</button>
          
      </form>

    </div>
    <div class="buttons">
      <div class="row">
        <div class="col">
          <button @click="updateDisplay('+')" class="btn">+</button>
          <button @click="updateDisplay('-')" class="btn">-</button>
          <button @click="updateDisplay('*')" class="btn">&times;</button>
          <button @click="updateDisplay('/')" class="btn">&divide;</button>
          <button @click="updateDisplay('^')" class="btn">^</button>
       
      
        </div>
      </div>

      <div class="row">
        <div class="col-auto">
          <button @click="updateDisplay('1')" class="btn">1</button>
          <button @click="updateDisplay('2')" class="btn">2</button>
          <button @click="updateDisplay('3')" class="btn">3</button>
          <button @click="updateDisplay('(')" class="btn">(</button>
        </div>
      </div>

      <div class="row">
        <div class="col-auto">
          <button @click="updateDisplay('4')" class="btn">4</button>
          <button @click="updateDisplay('5')" class="btn">5</button>
          <button @click="updateDisplay('6')" class="btn">6</button>
           <button @click="updateDisplay(')')" class="btn">)</button>
        </div>
      </div>

      <div class="row">
        <div class="col-auto">
          <button @click="updateDisplay('7')" class="btn">7</button>
          <button @click="updateDisplay('8')" class="btn">8</button>
          <button @click="updateDisplay('9')" class="btn">9</button>
          <button @click="deleteDigit" class="btn">DEL</button>
          
     
        
        </div>
      </div>

      <div class="row">
        <div class="col-auto">
        
            <button class="btn" @click="clearDisplay">C</button>
          <button @click="updateDisplay('.')" class="btn">.</button>
               <button @click="updateDisplay('0')" class="btn">0</button>
           
              
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { evaluate } from 'mathjs';

export default {
  data() {
    return {
      inputStr: '',
      result: '',
    };
  },
  methods: {
    updateDisplay(val) {
      this.inputStr += val;
    },
    calculate() {
      if (this.inputStr.trim() === '') {
        this.result = '';
      } else {
        try {
          this.result = String(evaluate(this.inputStr));
        } catch (error) {
          this.result = 'Error';
        }
      }
      this.inputStr = '';
    },
    clearDisplay() {
      this.inputStr = '';
      this.result = '';
    },
     deleteDigit() {
    this.inputStr = this.inputStr.slice(0, -1);
  }
  },
  
};
</script>

<style>
.calculator {
  width: 300px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 15px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #f0f0f0;
}

.display {
  margin-bottom: 10px;
}

.result {
  font-size: 24px;
  font-weight: bold;
  text-align: right;
  margin-bottom: 10px;
}

.buttons {
  display: flex;
  flex-wrap: wrap;
}

.row {
  margin-bottom: 10px;
}

.col {
  display: flex;
  justify-content: space-around;
}

.col-auto {
  display: flex;
  flex-direction: column;
}

.btn {
  padding: 15px 20px;
  margin: 5px;
  font-size: 20px;
  cursor: pointer;
  background-color: #e0e0e0;
  color: #444;
  border: 1px solid #bbb;
  border-radius: 12px;
  transition: all 0.3s ease;
}

.btn:hover {
  background-color: #ccc;
}

.btn:active {
  transform: scale(0.95);
}

input[type="text"] {
  width: calc(100% - 80px);
  padding: 10px;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  background-color: #f8f8f8;
}

button[type="submit"] {
  padding: 15px 20px;
  font-size: 20px;
  border: none;
  border-radius: 12px;
  background-color: #3498db;
  color: #fff;
  transition: all 0.3s ease;
}

button[type="submit"]:hover {
  background-color: #2980b9;
}

button[type="submit"]:active {
  transform: scale(0.95);
}

</style>