<template>
  <div class="component">
    <h3>You may view the User Details here</h3>
    <p>Many Details</p>
    <p>Username: {{name}}</p>
    <p>User Age: {{userAge}}</p>
    {{logName()}}
    <button @click="resetName">Reset Name</button>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  props: {
    name: {
      type: [String, Array],
      required: true,
    },
    userAge: Number,
  },
  data: function () {
    return {
      myName: this.name,
    };
  },
  methods: {
    logName: function () {
      // Max passed in from the parent component
      console.log(this.name);
    },
    resetName() {
      this.name = "Max";
      this.$emit("nameWasReset", this.name);
    },
  },
  created() {
    eventBus.$on("ageWasEdited", (age) => {
      this.userAge = age;
    });
  },
};
</script>

<style scoped>
div {
  background-color: lightcoral;
}
</style>
