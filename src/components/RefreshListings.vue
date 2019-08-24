<template>
  <div>
    <form @submit="refreshListings">
      <input type="submit" value="Get listings" class="btn" />
    </form>
  </div>
</template>

<script>
export default {
  name: "RefreshListings",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    refreshListings(e) {
      e.preventDefault(); // Dont want to submit the file. Prevent default behavior

      //Send up to parent
      this.$emit("refresh-listings");
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
  padding: 5px;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
}

input[type="submit"] {
  flex: 2;
}
</style>
