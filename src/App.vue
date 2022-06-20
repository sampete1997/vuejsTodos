<script>
import axios from 'axios';

export default {

  data() {
    return {
      search: "",
      posts: [],
      users: [],
      userNameObj: {}

    }
  },

  mounted() {

    axios
      .get('https://jsonplaceholder.typicode.com/users')
      .then(response => response.data)
      .then(data => {


        data.map((currUser) => {

          return this.userNameObj[currUser.id] = currUser.name
        })

        console.log('user', this.userNameObj);
        return (this.users = data)
      })
      .catch((err) => console.log('err:', err))

    axios
      .get('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.data)
      .then(data => {
        console.log('fetched data', data);
        return (this.posts = data)
      })
      .catch((err) => console.log('err:', err))


  },
  computed: {
    filteredPosts() {
      return this.posts.filter(post =>
        post.title.toLowerCase().includes(this.search.toLowerCase())
      );
    }
  }
}
</script>

<template >
  <div class="container">
    <input class="searchInput" type="text" placeholder="search" v-model="search" />
    <v-layout v-for="item in filteredPosts" :key="item.title">
      <v-card class="card">
        <div>

          <h2>{{ userNameObj[item.userId] }}</h2>
          <h3>{{ item.title }}</h3>
          <h4>{{ item.body }}</h4>
        </div>
      </v-card>
    </v-layout>

  </div>

</template>

<style>


.card {
  /* background-image: linear-gradient(rgb(253, 253, 253),rgb(243, 221, 179), rgb(0, 72, 255)); */
  width: 70%;
  margin: 0 auto;
  padding: 1rem;
  margin-bottom: 2rem;
  margin-top: 2rem;
}

.card div {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}



h4 {
  margin-top: 1.5rem;
  color: rgba(7, 7, 7, 0.63);
  font-weight: 900;
}

h3 {
  margin-top: 1.5rem;
    color: rgba(7, 7, 7, 0.795);

}


.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.699);
}

.searchInput {
  margin-top: 2rem;
  border: 1px solid rgba(0, 0, 0, 0.425);
  width: 40%;
  background-color: white;
  padding: 0.3rem;
}
</style>

















<!-- <template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script> -->
