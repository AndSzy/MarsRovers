<template>
  <div id="rovers-container">
    <the-card
      v-for="rover in rovers"
      :key="rover.name"
      width="w-100"
      :header="rover.name"
    >
      {{ rover.state }}
    </the-card>
  </div>
</template>

<script>
import TheCard from "./TheCard.vue";

export default {
  name: "TheDashboard",
  components: {
    TheCard,
  },
  props: {
    rovers: {
      type: Array,
    },
  },
};
</script>

<style>
#rovers-container {
  padding: 30px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
  margin-bottom: 60px;
}

@media (max-width: 900px) {
  #rovers-container {
    padding: 10px;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
}

@media (max-width: 500px) {
  #rovers-container {
    padding: 10px;
    grid-template-columns: 1fr;
    gap: 10px;
  }
}
</style>