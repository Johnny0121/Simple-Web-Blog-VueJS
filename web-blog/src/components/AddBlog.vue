<template>
  <div id="add-blog">
      <h2>Add a new Blog Post</h2>
      <form action="" v-if="!submitted">
          <label for="blogTitle">Blog Title:</label>
          <input type="text" v-model.lazy="blog.title" required>
          <label for="blogContent">Blog Content:</label>
          <textarea name="blogContent" v-model.lazy="blog.content" id=""></textarea>
          <div id="checkboxes">
              <label for="">Ninjas</label>
              <input type="checkbox" value="ninjas" v-model="blog.categories">
              <label for="">Wizard</label>
              <input type="checkbox" value="wizard" v-model="blog.categories">
              <label for="">Mario</label>
              <input type="checkbox" value="mario" v-model="blog.categories">
              <label for="">Cheese</label>
              <input type="checkbox" value="cheese" v-model="blog.categories">
          </div>
          <label for="author">Author</label>
          <select v-model="blog.author">
              <option v-for="author in authors" v-bind:key="author.id">{{ author }}</option>
          </select>
          <button v-on:click.prevent="post">Add Blog</button>
      </form>

      <div v-if="submitted">
          <h3>Thanks for adding your post!</h3>
      </div>

      <div id="preview">
          <h3>Preview Blog</h3>
          <p>Blog Title: {{ blog.title }}</p>
          <p>Blog Content:</p>
          <p>{{ blog.content }}</p>
          <p>Blog Categories:</p>
          <ul>
              <li v-for="category in blog.categories" v-bind:key="category.id">{{ category }}</li>
          </ul>
          <p>Author: {{ blog.author }}</p>
      </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'AddBlog',
  data() {
    return {
        blog: {
            author: '',
            title: '',
            content: '',
            categories: []
        },
        authors: ['Pink Man', 'ProZD', 'Electric Boogaloo', 'Treeboi'],
        submitted: false
    }
  },
  methods: {
      post: function(){
          axios.post('https://jsonplaceholder.typicode.com/posts', {
              title: this.blog.title,
              body: this.blog.content,
              userId: 1
          })
          .then(response => {
              console.log(response);
              this.submitted = true;
          });
      }
  }
}
</script>

<style>
#add-blog *{
    box-sizing: border-box;
}
#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}
#checkboxes input{
    display: inline-block;
    margin-right: 10px;
}
#checkboxes label {
    display: inline-block;
}
</style>
