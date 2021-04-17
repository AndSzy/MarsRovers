<template>
  <div class="home">
    <the-header id="header"></the-header>
    <the-dashboard
      v-if="!loading"
      :rovers="rovers"
      :loading="loading"
    ></the-dashboard>
    <the-footer id="footer"></the-footer>
    <router-view id="modal" @cancel="goHome" @launch="newRover"></router-view>
  </div>
</template>

<script>
import TheHeader from "../components/TheHeader.vue";
import TheFooter from "../components/TheFooter.vue";
import TheDashboard from "../components/TheDashboard.vue";

export default {
  name: "Home",
  components: {
    TheHeader,
    TheFooter,
    TheDashboard,
  },
  data() {
    return {
      rovers: null,
      loading: true,
      errored: false,
    };
  },
  methods: {
    getRovers() {
      this.axios
        .get("http://localhost:4444/rovers")
        .then((response) => (this.rovers = response.data))
        .catch((error) => {
          console.log(error);
          this.errored = true;
        })
        .finally(() => (this.loading = false));
    },
    postRovers(newRoverName) {
      let myThis = this;
      this.axios
        .post(`http://localhost:4444/add-rover/${newRoverName}`, {})
        .then(function (response) {
          myThis.getRovers();
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    newRover(newRoverName) {
      this.postRovers(newRoverName);
      this.goHome();
    },
    goHome() {
      this.$router.push("/");
    },
  },
  created() {
    this.getRovers();
  },
};
</script>

<style>
.home .bg-info {
  background-color: white !important;
}
#header {
  border-bottom: 1px solid black;
}

#footer {
  border-top: 1px solid black;
}
#modal {
  position: fixed;
  background-color: #f7f7f7;
  left: 50%;
  transform: translateX(-300px);
  top: 20vh;
  z-index: 100000;
  width: 600px;
}

@media (max-width: 600px) {
  #modal {
    width: 100%;
    transform: translateX(0);
    left:0;
    right:0;
    top:0;
    bottom:0;
  }
}


</style>
