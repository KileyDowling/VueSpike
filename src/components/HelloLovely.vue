<template>
  <div class="hello">
   <div class="intro"> <h2>{{ msg }} <span class="name">{{name}}</span></h2></div>

      <p>Set/Update your goal:
  <input v-model="goal"  type="number" placeholder="enter your goal here" /> </p>
  <h3><b>Your goal is <span style="color: green">${{goal}}</span></b></h3>

  <p> Previous Balance: ${{previousProgress}}  <span v-if="previousProgress!=getLatest || getLatest==0 "> | Current Balance: ${{getLatest}}</span></p>

 <p>Make a deposit: <input v-model="addedValue" type="number" placeholder="add your latest deposit" /> </p>

  <div class="reverseProgress">
    <!--<p class="progress">Congrats! You are now at {{percentProgress}} of your goal</p> -->

  <p>Amount Remaining: <span id="goal">{{remainingToGoal}} </span>| Percent Remainng: <span id="percent">{{remainingToGoalPercent}}</span></p></div>
    </div>
</template>

<script>
export default {
  name: "HelloLovely",

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
      default: 25
    },
    goal: {
      type: Number,
      default: 100
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
    calculatePercentToGoal: function() {
      this.percentToGoal = Math.round((this.latest / this.goal) * 100);
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
</style>
