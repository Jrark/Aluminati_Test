<template>
  <div>
    <!-- Added paragraph here to more clearly indicate intention and result to user. -->
    <h2>
      The list of all numbers in your number. You can then mouse over them to
      find their divisible values.
    </h2>
    <div
      class="number"
      :id="'number-' + number"
      v-for="number in n"
      :key="number"
      @mouseover="hov(number)"
      @mouseout="reset"
    >
      {{ number }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      limit: this.$parent.limit,
      numbers: []
    };
  },
  watch: {
    ["$parent.limit"](newLimit) {
      this.limit = newLimit;
    }
  },
  methods: {
    hov(number) {
      const nums = document.querySelectorAll(".number");
      for (let i = 0; i < nums.length; i++) {
        const num = nums[i].textContent.trim();
        if (number % num === 0) {
          nums[i].classList.add("active");
          /* Console log could be removed in the final version of release. */
          /* Console.log('divisor', num) */
        }
      }
    },
    reset() {
      const nums = document.querySelectorAll(".number");
      nums.forEach(num => num.classList.remove("active"));
    }
  },
  /* Add computed section and moved method n() in so as to ensure n() is not called unnecessarily. */
  computed: {
    n() {
      let numbers = [];
      // Started incrementing from 1 as well as increasing the upper limit to include the number the user typed with the <=.
      for (var i = 1; i <= this.limit; i++) {
        numbers = [...numbers, i];
      }
      return numbers.sort(() => Math.random() - 0.5);
    }
  }
};
</script>

<style scoped>
.number {
  color: #e8e8e8;
  display: inline-block;
  padding: 5px;
  background-color: #96939b;
  margin: 5px;
  /* Adjusted CSS to improve visuals */
  width: 5%;
  height: 30px;
  text-align: center;
  border-radius: 25px;
  padding-top: 1em;
  font-family: "Merienda", Helvetica, Arial;
}

.active {
  /* Adjusted CSS to improve visuals */
  color: white;
  background-color: #fc814a;
}
h2 {
  /* Adjusted CSS to improve visuals */
  color: #564256;
  font-family: "Merienda", Helvetica, Arial;
}
</style>
