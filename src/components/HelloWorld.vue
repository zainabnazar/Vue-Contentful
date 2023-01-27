<template>
  <div class="hello">
    <div v-if="theContents">
      <h2>{{ theContents }}</h2>
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      theContents: [],
    };
  },
  methods: {
    getContents() {
      axios
        .get(
          `https://cdn.contentful.com/spaces/${process.env.VUE_APP_SPACEID}/environments/master/entries?access_token=${process.env.VUE_APP_ACCESSTOKEN}`
        )
        .then((res) => {
          this.theContents = JSON.stringify(res.data.items[0].fields.name);
          console.log(this.theContents);
        });
      return this.theContents;
    },
  },
  mounted() {
    this.getContents();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
