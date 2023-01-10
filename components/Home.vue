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
      <h2>Interesting Fact</h2>
      <h3>{{ fact }}</h3>
      <NuxtLink to="/about">About</NuxtLink>
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
        // Incase there is no connection
        if (
          !window.navigator.onLine &&
          !error.response &&
          error.code === "ERR_NETWORK"
        ) {
          this.fact = "Please check your connection";

          // Listen for when we are back online
          window.addEventListener("online", (e) => {
            this.fact = "Back online... Give me a sec";
            // Fetch the fact when we are back online
            setTimeout(() => {
              this.fetchFact(number);
            }, 2000);
          });
        }
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
