<template>
  <div class="search">
    <form @submit="getWeather">
      <div class="form-control">
        <input type="text" id="city" v-model="city" placeholder="City..." />
      </div>

      <div class="form-control">
        <input
          type="text"
          id="country"
          v-model="country"
          placeholder="Country Code (e.g. UK)..."
        />
      </div>

      <button
        type="submit"
        class="btn"
        :disabled="city === '' || country === ''"
      >
        Get Weather
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Search",

  data() {
    return {
      city: "",
      country: "",
    };
  },

  methods: {
    getWeather(e) {
      e.preventDefault();

      this.$emit("get-weather", this);
      this.city = this.country = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.btn {
  width: 100%;
}
.form-control {
  margin: 10px 0;
}
input[type="text"] {
  font-size: 1.2em;
  opacity: 0.5;
  width: 100%;
  padding: 0.9em 0.5em;
  outline: none;
  border: none;
  border-radius: 12px 2px 12px 2px;

  transition: 0.3s ease;

  &:hover {
    opacity: 0.8;
  }

  &:focus {
    opacity: 1;
    border-radius: 2px 12px 2px 12px;
  }
}
</style>
