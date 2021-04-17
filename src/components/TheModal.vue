<template>
  <the-card header="New Rover">
    <b-form class="mb-4">
      <p>Launch new rover to mars</p>
      <b-form-input
        id="new-rover"
        v-model="newRoverName"
        placeholder="Rover Name"
      ></b-form-input>
    </b-form>

    <b-button @click="cancel">Cancel</b-button>
    <b-button @click="launch">Launch</b-button>
  </the-card>
</template>

<script>
import TheCard from "./TheCard.vue";
export default {
  name: "TheModal",
  components: {
    TheCard,
  },
  data() {
    return {
      newRoverName: "",
    };
  },
  methods: {
    cancel() {
      this.$emit("cancel");
    },
    launch() {
      if (this.newRoverName) {
        this.$emit("launch", this.newRoverName);
      } else {
          alert("Enter Rover Name")
      }
      
    },
  },
};
</script>

<style>
</style>