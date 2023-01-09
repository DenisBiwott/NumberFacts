<template>
  <div>
    <div class="main-div">
      <h1>NUMBER FACT CHECKER</h1>
      <countTo
        :startVal="startVal"
        :endVal="endVal"
        :duration="duration"
      ></countTo>
      <Fact @submit="doCounter" />
      <h2>Interesting Fact 😏</h2>
      <h3>{{ fact }}</h3>
    </div>
  </div>
</template>

<script>
import countTo from "vue-count-to";
import Fact from "~/components/Fact";
export default {
  components: {
    countTo,
    Fact,
  },
  data() {
    return {
      // Make this dynamic so we start from the previously entered value
      // Set value to the previous edVal value on next mount
      startVal: 0,
      endVal: 0,
      duration: 1000,
      fact: "Wait...",
    };
  },
  methods: {
    // Does the counter thingy and calls the api call method
    // by changing the end Value
    doCounter(number) {
      this.endVal = parseInt(number);
      // Call the API method
      this.fetchFact(number);
    },

    //Does the API call to fetch the fact
    async fetchFact(number) {
      this.fact = "Thinking...";
      try {
        // TODO: Find a way to check if there is no connection
        const res = await this.$axios.get(`http://numbersapi.com/${number}`);
        this.fact = res.data;
      } catch (error) {
        console.log(error.message);
        throw error.message;
      }
    },
  },
};
</script>

<style>
input {
  text-align: center;
  margin-top: 5px;
  margin-right: 10px;
}
.main-div {
  padding: 20px;
  background-color: lightgray;
  text-align: center;
}
</style>
