<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Vue.js 2 and Firebase Sample Application</h1>
    </div>

  <div class="panel panel-default">
    <div class="panel-heading">
      <h3>Add a Book</h3>
    </div>
    <div class="panel-body">
      <form id="form" class="form-inline" v-on:submit.prevent="addBook">
        <div class="form-group">
          <label for="bookTitle">Title: </label>
          <input type="text" id="bookTitle" class="form-control" v-model="newBook.title">
        </div>
        <div class="form-group">
          <label for="bookAuthor">Author: </label>
          <input type="text" id="bookAuthor" class="form-control" v-model="newBook.author">
        </div>
        <div class="form-group">
          <label for="bookUrl">URL: </label>
          <input type="text" id="bookUrl" class="form-control" v-model="newBook.url">
        </div>
        <input type="submit" class="btn btn-primary" value="Add Book">
      </form>
    </div>
  </div>

    <div class="panel pannel-default">
      <div class="panel-heading">
        <h3>Books List</h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>Title</th>
              <th>Author</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="book in books" v-bind:key="book.id">
              <td><a v-bind:href="book.url">{{book.title}}</a></td>
              <td>{{book.author}}</td>
              <td><span class="glyphicon glyphicon-trash" v-on:click="deleteBook(book)"></span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import Firebase from "firebase";

let config = {
  apiKey: "AIzaSyA3NlACgVWGaM6Y15jT5lazlMzXD49bVdg",
  authDomain: "vuefirebase-tutorial.firebaseapp.com",
  databaseURL: "https://vuefirebase-tutorial.firebaseio.com",
  projectId: "vuefirebase-tutorial",
  storageBucket: "vuefirebase-tutorial.appspot.com",
  messagingSenderId: "1076432486408"
};

let app = Firebase.initializeApp(config);
let db = app.database();

let bookRef = db.ref("books");

export default {
  name: "app",
  firebase: {
    books: bookRef
  },
  data() {
    return {
      newBook: {
        title: "",
        author: "",
        url: ""
      }
    };
  },
  methods: {
    addBook: function() {
      bookRef.push(this.newBook);
      this.newBook.title = "";
      this.newBook.author = "";
      this.newBook.url = "";
    },
    deleteBook: function(book) {
      bookRef.child(book[".key"]).remove();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
