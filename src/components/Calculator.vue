<template>
<div class="calculator">
    
    <!-- if display num is an empty string -->
    <div class="display" v-if="displayNum == ''"> 0 </div>
    <!-- display is not a empty string, therfore display it. -->
    <div class="display" v-else> {{ displayNum }} </div> 
    <div @click ="clear()" class="btn">C</div> 
    <div @click ="changeSign()" class="btn">+/-</div>
    <div @click ="precent()" class="btn">%</div>
    <div @click ="division()" class="btn operator">÷</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click ="multiplication()" class="btn operator">x</div>
    <div @click="append(4)"  class="btn">4</div>
    <div @click="append(5)"  class="btn">5</div>
    <div @click="append(6)"  class="btn">6</div>
    <div @click ="subtraction()" class="btn operator">-</div>
    <div @click ="append(1)"  class="btn">1</div>
    <div @click ="append(2)"  class="btn">2</div>
    <div @click ="append(3)"  class="btn">3</div>
    <div @click ="addition()" class="btn operator">+</div>
    <div @click ="append(0)"  class="btn zero">0</div>
    <div @click ="dot()" class="btn">.</div>
    <div @click = "equals()"  class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      /* 
      * displayNum - Used to display and 
        store(numbers will be added as a string to the end) 
        the final calculation to the user  
      * current - Used to get the current number entered
      * previous - Used to the previous number entered
      * calculate - Uses the displayNum(the numbers entered by the user)
      *             to calcuate the answer
      * lastOperator - Will be used lastOperator
      */
      displayNum: '',
      current: null,
      previous: null,
      calculate: null,
      lastOperator: ''
    }
  },
  methods: {
    /* clear - will clear the display and 
     * Assign all vars to their default value */
    clear(){
      this.displayNum = '';
      this.current = null;
      this.previous = null;
      this.calculate = null;
      this.lastOperator = '';
    },
    /* append(num) - Uses the parameter num to    
    *  to add to the end of displayNum string
    */
    append(num){
      /*  If the user hasen't entered a number before
      *   the previous number will be null   
      */ 
      if(this.previous == null){
        /*   Assign num and previous(beucase 
        *    the user hasn't entered a number before )   
        *    to num
        */ 
        this.current = num;
        this.previous = num;

        //Output current to user
        this.displayNum = this.current.toString();
      }

      /*  else the previous is not equal null
      *   (the user has entered a number before)
      */
      else{
        //Assign previous to current 
        this.previous = this.current;

        ///Assign current to num 
        this.current = num;
        
          /*  If the displayNum string is greater than or 
          *   equal to two, then
          *   the user wants a number with or equal to  
          *   two places 
          */
          if(this.displayNum.length >= 2){
            this.displayNum =  this.displayNum + this.current.toString();
          }
          // Add another numberdight(previous and current) to the displayNum
          else{
            this.displayNum = this.previous.toString() + this.current.toString();
          }
      }
    },
    // dot - the user wants to input a decimal number
    dot(){
      
      // Add the decimal to the end of the input
      this.current = this.displayNum + '.';
      
      // Display the current number
      this.displayNum = this.current;
    }, 

    /* changeSign - 
    *  change the input number from a 
    *  negative to positive or a 
    *  positive to a negative number
    */
    changeSign(){
      // Assign current and previous to null 
      this.current = null;
      this.previous = null;
      
      //  Set the displayNum to be the opposite 
      this.calculate = parseFloat(-this.displayNum);

      //  DisplayNum the opposite number
      this.displayNum = this.calculate;
    },
    
      // precent - Calculate the precent of the input number
    precent(){

      //  Assign current and previous to null values
      this.current = null;
      this.previous = null;

      //  Calculate the precent of the input number
      this.calculate = parseFloat(this.displayNum) / 100;

      //  Display the precent to the user
      this.displayNum = this.calculate.toString();
    },
      // division - Calculate division from the input
     division(){

      // The lastOperator that was used was division
      this.lastOperator = 'divi';
      
      // Assign current and previous to null
      this.current = null;
      this.previous = null;

      // If the calculate is null
      if(this.calculate == null){
        // Assign calculate to displayNum  
         this.calculate = parseFloat(this.displayNum);
      }

      // else the calculate is not null
      else{
       // Assign calculate to its self and displayNum
         this.calculate = (this.calculate) /  parseFloat(this.displayNum);
      }
      // Assign displayNum as calculate
      this.displayNum = this.calculate;
      
      // console.log the result 
      console.log("Calculate " + this.calculate)
    },

       // multiplication - Calculate multiplication from the input
      multiplication(){
      
      // The lastOperator that was used was multiplication 
      this.lastOperator = 'mult';

      // Assign current and previous to null
      this.current = null;
      this.previous = null;

      // If the calculate is null
      if(this.calculate == null){
         this.calculate = parseFloat(this.displayNum);
      }

      // else the calculate is not null
      else{
         // Assign calculate to its self and displayNum
         this.calculate = parseFloat(this.displayNum) * this.calculate;
      }
       // Assign displayNum as calculate
      this.displayNum = this.calculate;

       // console.log the result
      console.log("Calculate " + this.calculate)
    },

    // subtraction - Calculate subtraction from the input
    subtraction(){

       // The lastOperator that was used was subtraction 
      this.lastOperator = 'sub';

      // Assign current and previous to null
      this.current = null;
      this.previous = null;

      // If the calculate is null
      if(this.calculate == null){
         this.calculate = parseFloat(this.displayNum);
      }

      // else the calculate is not null
      else{
         // Assign calculate to its self and displayNum
          this.calculate =  this.calculate - parseFloat(this.displayNum);
      }
       // Assign displayNum as calculate
      this.displayNum = this.calculate;

       // console.log the result
      console.log("Calculate " + this.calculate)
    },

    // addition - Calculate subtraction from the input
    addition(){
       
       // The lastOperator that was used was subtraction 
      this.lastOperator = 'add';

      // Assign current and previous to null
      this.current = null;
      this.previous = null;

      // If the calculate is null
      if(this.calculate == null){
         this.calculate = parseFloat(this.displayNum);
      }

      // else the calculate is not null
      else{
         // Assign calculate to its self and displayNum
          this.calculate =  this.calculate + parseFloat(this.displayNum);
      }
       // Assign displayNum as calculate
      this.displayNum = this.calculate;

       // console.log the result
      console.log("Calculate " + this.calculate)
 
    },

    // equals - Used when the user clicks on the equal sign 
    equals(){

        // if the lastOperator was add
        if(this.lastOperator == "add" ){

          // Calculate the final result 
          this.calculate = this.calculate + parseFloat(this.displayNum);
        }

         // if the lastOperator was sub
        else if(this.lastOperator == "sub"){

          // Calculate the final result 
          this.calculate =  this.calculate - parseFloat(this.displayNum);
        }

        // if the lastOperator was mult
        else if(this.lastOperator == "mult"){

          // Calculate the final result 
          this.calculate = parseFloat(this.displayNum) * this.calculate;
        }

       // if the lastOperator was divi
         else if(this.lastOperator == "divi"){

           // Calculate the final result 
          this.calculate = (this.calculate) /  parseFloat(this.displayNum);
        }
        // Output the result
         this.displayNum = this.calculate.toString();
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  /* stylize the calculator element */
 .calculator {
  
  /* creates grid */ 
  display: grid;

  /* Set the width and height of the calculator */ 
  width:  400px;
  height: 350px;

  /* Set the marign and font size */ 
  margin: auto;
  font-size: 45px;
 
  /* Each column resizes itself automatically */
  grid-template-columns: auto;
  
  /* Each row resizes itself automatically */
  grid-auto-rows: auto;
}

  /* stylize the display element */
.display {

  /* start at grid line 1 and end at grid line 5 */
  grid-column: 1 / 5;
  
  /* set the background color */
  background-color:#3CB371;

  /* Set the color for the number */
  color: white;
}

/* stylize the display calculator */
.zero {
  /* start at grid line 1 and end at grid line 3 */
  grid-column: 1 / 3;
}

/* stylize the btn calculator */
.btn {
  /* stylize the background color */
  background-color: #BEBEBE;

  /* set the border as 1 px and set the color as #999 */
  border: 1px solid #999;
}

/* stylize the btn:active(btn has been clicked) */
.btn:active{
    /*stylize the background color */
    background: #858381;
}

/* stylize the operators */
.operator {
  
  /* stylize the background color */
  background-color: orange;

  /* stylize the operator color */
  color: #ffffff;
}
</style>