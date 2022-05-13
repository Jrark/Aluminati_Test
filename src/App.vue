<template>
  <div id="app">
    <!-- Added paragraph here to more clearly indicate intention to user. -->
    <h2>Enter whatever whole number you want:</h2>
    <!-- Added min and max for best practice. -->
    <input type="number" v-model="limit" min="1" max="100" />
    <Numbers />
  </div>
</template>

<script>
import Numbers from "@/components/Numbers";

export default {
  name: "App",
  components: { Numbers },
  data() {
    return {
      limit: 100
    };
  },
  // Added new watcher to ensure that if values get set above 100 or below 1 it will reset to 100 or 1.
  watch: {
    limit(newLimit) {
      if (newLimit > 100) {
        this.limit = 100;
      } else if (newLimit < 1) {
        this.limit = 1;
      }
      // Find a way to prevent decimals.
      else {
        this.limit = newLimit;
      }
    }
  }
};
</script>

<style scoped>
/* Adjusted CSS to improve visuals  */
template {
  background-color: #e8e8e8;
}
input {
  color: #564256;
  width: 20%;
  font-size: x-large;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  text-align: right;
  text-indent: 5px;
}
h2 {
  color: #564256;
  font-family: "Merienda", Helvetica, Arial;
}
</style>