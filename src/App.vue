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
  background-color: rgba(0, 0, 0, 0.055);
}

.searchInput {
  margin-top: 2rem;
  border: 1px solid rgba(0, 0, 0, 0.425);
  width: 40%;
  background-color: white;
  padding: 0.3rem;
}
</style>
