<template>
  <Header />
  <h1>Hello User ,Welcome on Add Restaurant Page</h1>
  <form class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter Name"
      v-model="restaurant.name"
    />
    <br />
    <input
      type="text"
      name="address"
      placeholder="Enter address"
      v-model="restaurant.address"
    />
    <br />
    <input
      type="text"
      name="contact"
      placeholder="Enter Name"
      v-model="restaurant.contact"
    />
    <br />
    <button type="button" v-on:click="addRestaurant">Add new Restaurant</button>
  </form>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Update",
  components: {
    Header,
  },
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
    async addRestaurant() {
      const result = await axios.post("http://localhost:3000/restaurant", {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      });
      if (result.status == 201) {
        this.$router.push({ name: "Home" });
      }
      console.warn("result", result);
    },
    mounted() {
      let user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
    },
  },
};
</script>