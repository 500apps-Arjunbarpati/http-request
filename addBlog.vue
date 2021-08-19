<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2>
    <form>
      <label>Blog title:</label>
      <input type="text" v-model="title" required />
      <label>Blog Content:</label>
      <textarea v-model="content"></textarea>
      <div id="checkboxes">
        <input type="checkbox" value="software" v-model="categories" />
        <label>software</label>
        <input type="checkbox" value="marketing" v-model="categories" />
        <label>marketing</label>
        <input type="checkbox" value="sales" v-model="categories" />
        <label>sales</label>
        <input type="checkbox" value="engineering" v-model="categories" />
        <label>engineering</label>
      </div>
      <img src="../assets/logo.png" />
      <label>Author</label>
      <select v-model="author">
        <option v-for="(author, index) in authors" :key="index">
          {{ author }}
        </option>
      </select>
      <button v-on:click.prevent="post">Add Blog</button>
    </form>
    <div v-if="submitted">
      <h3>Thanks for Adding post</h3>
      </div>
    <div id="preview">
      <h3>preview Blog</h3>
      <p>Blog title:{{ title }}</p>
      <p>Blog Content:{{ content }}</p>
      <p>Blog Categories</p>
      <ul>
        <li v-for="(category, index) in categories" :key="index">
          {{ category }}
        </li>
        <p>Author:{{ author }}</p>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      content: "",
      categories: [],
      author: "",
      authors: ["software", "marketing", "sales", "engineering"],
      submitted:false,
      
    };
  
  },
  methods:{
    post:function(){
      this.$http.post('https://jsonplaceholder.typicode.com/posts',{
        title:this.title,
        body:this.content,
        userId:1
      }).then(function(data){
        console.log(data);
      });
    }
  }
  
};

</script>

<style>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  margin: 20px auto;
  max-width: 500px;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}
#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}
#checkboxes label {
  display: inline-block;
}
</style>

