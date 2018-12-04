<template>
  <div class="posts">
    <h1>Posts</h1>
    <div v-if="posts.length > 0" class="table-wrap">
      <div>
        <router-link v-bind:to="{ name: 'NewPost' }" >Add Post</router-link>
      </div>
      <table>
        <tr>
          <td>Title</td>
          <td width="550">Description</td>
        </tr>
        <tr v-for="post in posts" :key="post.id">
          <td>{{ post.title }}</td>
          <td>{{ post.description }}</td>
        </tr>
      </table>
    </div>
    <div v-else>
      There are no posts.. Lets add one now <br /><br />
      <router-link v-bind:to="{ name: 'NewPost' }" class="add_post_link">Add Post</router-link>
    </div>
  </div>
</template>

<script>
import PostsService from '@/services/PostsService'
export default {
  name: 'posts',
  data () {
    return {
      posts: []
    }
  },
  mounted () {
    this.getPosts()
  },
  methods: {
    async getPosts () {
      const response = await PostsService.fetchPosts()
      this.posts = response.data.posts
      console.log('SHOW POST:', this.posts)
    }
  }
}
</script>

<style type="text/css">
.table-wrap {
  width: 70%;
  margin: 0 auto;
  text-align: center;
}

table{
  margin: 10px;
}
table th, table tr {
  text-align: left;
}

table tr td {
  padding: 10px;
}

table tr:nth-child(even) {
  background: #f2f2f2;
}

table tr:nth-child(1) {
  background: black;
  color: #fff;
}

a {
    background-color: #4d7ef7;
    border: none;
    color:  white;
    padding: 8px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 13px;
    margin: 0px -1px;
    border-radius: 15px;
    width: 148px;
}

a.add_post_link {
  background: black;
  color: #fff;
  padding: 10px 80px;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: bold;
}

</style>
