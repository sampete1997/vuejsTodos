
<template >
  <div class="container">
    <input class="searchInput" type="text" placeholder="Search" v-model="search" />
    <div v-for="item in filteredPosts" :key="item.title">
      <v-card class="card" max-width="600">
        <div>
          <h2>{{ userObj[item.userId] }}</h2>
          <h3>{{ item.title }}</h3>
          <h4>{{ item.body }}</h4>
        </div>
      </v-card>

    </div>

  </div>

</template>

<script>
import axios from 'axios';

export default {

  data() {
    return {
      search: "",
      posts: [],
      users: [],
      userObj: {}

    }
  },
  created() {

    this.fetchUserData()
      .then(response => response.data)
      .then(data => {

        data.map((currUser) => {

          return this.userObj[currUser.id] = currUser.name
        })

        console.log('user', this.userObj);
        return (this.users = data)
      })
      .catch((err) => console.log('err:', err))

    this.fetchPostData()
      .then(response => response.data)
      .then(data => {
        console.log('fetched data', data);
        return (this.posts = data)
      })
      .catch((err) => console.log('err:', err))

  },

  methods: {

    fetchUserData() {
      return axios.get('https://jsonplaceholder.typicode.com/users')
    }
    ,
    fetchPostData() {
      return axios.get('https://jsonplaceholder.typicode.com/posts')
    }


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

<style>
.v-card {
  background-image: url('https://thumbs.dreamstime.com/z/old-paper-flower-background-frame-4289123.jpg');
  background-size: cover;
  margin: 0 auto;
  padding: 1rem;
  margin-bottom: 2rem;
  margin-top: 2rem;
  height: auto;

}

.v-card:hover {
  transform: scale(1.1);
}

.card div {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

h2 {
  color: red
}

h4 {
  margin-top: 1.5rem;
  color: rgba(0, 0, 0, 0.925);
  font-weight: 900;
}

h3 {
  margin-top: 1.5rem;
  color: rgba(7, 7, 7, 0.904);

}


.container {
  display: flex;
  flex-direction: column;
  align-items: center;

}

.searchInput {
  margin-top: 2rem;
  border: 1px solid rgba(0, 0, 0, 0.425);
  width: 50%;
  background-color: rgba(218, 218, 218, 0.226);
  padding: 0.4rem;
  border-radius: 0.5rem;
}
</style>
