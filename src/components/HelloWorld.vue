<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <!-- <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul> -->
  </div>
</template>

<script>
// import { Socket } from '../phoenix.js'
import { Socket } from "phoenix";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  created() {
    var token = "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhYmlsaXRpZXMiOltdLCJhdWQiOiI5MGQiLCJleHAiOjE2MjE0MjYxMzEsImlhdCI6MTYxOTAwNjkzMSwiaXNzIjoiOTBkIiwianRpIjoiZDExZjUyYTUtODk3NS00MDE3LTkyNzQtYzliZGFiOTQwMTU2IiwibmJmIjoxNjE5MDA2OTMwLCJyb2xlcyI6WyJzdXBlcmFkbWluIl0sInN1YiI6IjEiLCJ0eXAiOiJhY2Nlc3MifQ.u2OO4aLfFGqLREnjI8yiTntHkiE9oEhVJ6kRQWMF_mw_891li9c2H60EOA4o2hzKjLuN2OkjOoVhjrPk_hFj8w"
    var socket = new Socket("ws://" + "localhost:4000" + "/socket",{params: {token: token}});
    socket.connect();
    let channel = socket.channel("notifications:1", {});
    channel
      .join()
      .receive("ok", (resp) => {
        console.log("Joined successfully", resp);
      })
      .receive("error", (resp) => {
        console.log("Unable to join", resp);
      });

    channel.on("new_msg", payload => {
      console.log("new_msg", payload)
})


  },
  computed: {


  }
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
