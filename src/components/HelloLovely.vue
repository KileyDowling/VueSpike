<template>
<div>
   <div class="intro"> 
     <input v-model="name"  type="text" placeholder="update your name" />
       <h2>{{ msg }} <span class="name">{{name}}</span></h2>
       </div>
<h3><p class="bold">Your goal is <span class="green">${{goal}}</span></p></h3>
      <p>Set/Update your goal:
  <input v-model="goal"  type="number" placeholder="enter your goal here" /> </p>
  

  <p> Previous Balance: ${{previousProgress}}  <span v-if="previousProgress!=getLatest || getLatest==0 "> | Current Balance: ${{getLatest}}</span></p>
  
 <p>Make a deposit: <input v-model="addedValue" type="number" placeholder="add your latest deposit" /> <button class="button" v-on:click="submitDeposit()">Add</button></p>

  <div class="reverseProgress">
    <p class="progress">Congrats! You are now at {{percentProgress}} of your goal</p> 

  <p>Amount Remaining: <span id="goal">{{remainingToGoal}} </span>| Percent Remainng: <span id="percent">{{remainingToGoalPercent}}</span></p></div> 


  <hr>
<p>Previous Deposits</p>
   <Deposit v-for="deposit in list" 
                    :deposit="deposit" 
                    :key="deposit.id" />

<p class="bold">Total Deposits: <span class="green">{{calculateDeposits()}}</span></p>
</div>
</template>

<script>
import Deposit from "./Deposit.vue";

export default {
  name: "HelloLovely",
  components: {
    Deposit
  },
  data() {
    return {
      list: [
        {
          id: 1,
          amount: 5500,
          date: new Date("January 1, 2018 9:20").toLocaleString()
        },
        {
          id: 2,
          amount: 500,
          date: new Date("February 1, 2018 14:45").toLocaleString()
        }
      ],
      deposit: ""
    };
  },

  props: {
    msg: {
      type: String,
      default: "Hello,"
    },
    name: {
      type: String,
      default: "Lovely"
    },
    previousProgress: {
      type: Number,
      default: 6000
    },
    goal: {
      type: Number,
      default: 10000
    },
    progress: Number,
    addedValue: {
      type: Number,
      default: 0
    },
    percentToGoal: Number,
    latest: {
      type: Number,
      default: 0
    }
  },

  methods: {
    formatter: function(num) {
      return new Intl.NumberFormat("en-US", {
        style: "currency",
        currency: "USD",
        minimumFractionDigits: 2
      }).format(num);
    },
    calculatePercentToGoal: function() {
      this.percentToGoal = Math.round((this.latest / this.goal) * 100);
    },
    calculateDeposits: function() {
      let sum = 0;
      this.list.forEach(function(item) {
        sum += parseFloat(item.amount);
      });

      return this.formatter(sum);
    }
  },

  computed: {
    // a computed getter
    getLatest: function() {
      let result = parseInt(this.previousProgress) + parseInt(this.addedValue);
      this.latest = result;
      return result;
    },
    percentProgress: function() {
      this.calculatePercentToGoal();
      return this.percentToGoal + "%";
    },
    remainingToGoal: function() {
      if (this.percentToGoal >= 100) {
        // document.getElementById("goal").style.fontStyle = "italic";
        return "Goal Achieved";
      } else {
        //document.getElementById("goal").style.fontStyle = "normal";
        var tot = this.goal - this.latest;
        return "$" + tot;
      }
    },

    remainingToGoalPercent: function() {
      this.calculatePercentToGoal();
      if (this.percentToGoal >= 100) {
        //document.getElementById("percent").style.fontStyle = "italic";
        return "Goal Achieved";
      } else {
        //document.getElementById("percent").style.fontStyle = "normal";
        return 100 - this.percentToGoal + "%";
      }
    },
    submitDeposit: function() {
      this.list.push({
        date: new Date(Date.now()).toLocaleString(),
        amount: this.addedValue
      });
      this.calculateDeposits();
      this.previousProgress = this.latest;
      this.addedValue = 0;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.name {
  color: pink;
  font-style: italic;
}
.progress {
  color: deeppink;
  font-weight: bold;
}
.reverseProgress {
  color: lightslategray;
  font-weight: bold;
}

.button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 3px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 0px 6px;
}
.green {
  color: green;
}
.bold {
  font-weight: bold;
}
</style>
