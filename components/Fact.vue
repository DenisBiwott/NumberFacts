<template>
  <div class="fact">
    <form @submit.prevent="onSubmit">
      <input v-model="num" placeholder="0" />
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
};
</script>

<style>
.fact {
  background-color: lightgray;
  text-align: center;
  padding: 5px;
}
</style>
