<template>
  <div class="fact">
    <form @submit.prevent="onSubmit">
      <input v-model="num" placeholder="0" ref="input" />
      <input type="submit" value="Get Fact" />
    </form>
    <br />
  </div>
</template>

<script>
export default {
  name: "Fact",
  data() {
    return {
      num: "",
    };
  },
  methods: {
    onSubmit() {
      this.$emit("submit", this.num);
    },
  },
  // Focus on the input field on mount
  mounted() {
    this.$refs.input.focus();
  },
};
</script>

<style>
.fact {
  background-color: lightgray;
  text-align: center;
  padding: 5px;
}
</style>
