<template>
  <div id="app">
    <Header />
    <RefreshListings v-on:refresh-listings="refreshListings" />
    <Todos v-bind:entries="entries" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import RefreshListings from "./components/RefreshListings";
import Todos from "./components/Todos";
import axios from "axios";
import qs from "qs";

export default {
  name: "app",
  components: {
    Header,
    Todos,
    RefreshListings
  },
  data() {
    return {
      entries: []
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => (this.entries = this.entries.filter(todo => todo.id !== id)))
        .catch(err => console.log(err));
    },
    refreshListings() {
      const headers = {
        "Accept": "*/*",
        "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",
        "DNT": 1,
        "Referer": "https://www.realtor.ca/map",
        "Sec-Fetch-Mode": "cors",
        "User-Agent":
          "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.100 Safari/537.36"
      };

      const instance = axios.create(headers);
      const targetUrl = "https://api2.realtor.ca/Listing.svc/PropertySearch_Post";

      const data = qs.stringify({
        ApplicationId: 1,
        CultureId: 1,
        Version: "7.0",
        CurrentPage: 1,
        BuildingTypeId: 2,
        TransactionTypeId: 2,
        RecordsPerPage: 200,
        PropertyTypeGroupID: 1,
        PropertySearchTypeId: 1,
        GeoIds: "g30_f2hf63p5"
      });

      instance
        .post(targetUrl, data)
        .then(res => {
          this.entries = res.data.Results;
        })
        .catch(err => console.log(`*** Error *** ${err}`));
    }
  },
  created() {
    // axios
    //   .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
    //   .then(res => (this.entries = res.data))
    //   .catch(err => console.log(err));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
