<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Vue.js 2 and Firebase Sample Application</h1>
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
            </tr>
          </thead>
          <tbody>
            <tr v-for="book in books" v-bind:key="book.id">
              <td><a v-bind:href="book.url">{{book.title}}</a></td>
              <td>{{book.author}}</td>
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
