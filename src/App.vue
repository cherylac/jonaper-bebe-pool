<template>
  <div id="app" class="container">
    <div class="page-header">
  <h1>What will IT be? And when will IT get here??</h1>
  </div>
  <div class="panel panel-default">
    <div class="panel-heading">
      <h3 class="panel-title">Enter Contest</h3>
    </div>
    <div class="panel-body">
      <form id="form" class="form-inline" v-on:submit.prevent="addEntry">
        <div class="form-group">
          <label for="entryContestant">Your name:</label>
          <input type="text" id="entryContestant" class="form-control" v-model="newEntry.contestant">
        </div>
        <div class="form-group">
          <label for="entryGirlorboy">Girl or Boy:</label>
          <input type="text" id="entryTitle" class="form-control" v-model="newEntry.gender">
        </div>
        <div class="form-group">
          <label for="bookUrl">Guess Date:</label>
          <input type="text" id="entryDate" class="form-control" v-model="newEntry.date">
        </div>
        <div class="form-group">
          <label for="entryWeight">Guess Weight:</label>
          <input type="text" id="entryWeight" class="form-control" v-model="newEntry.weight">
        </div>
        <div class="form-group">
          <label for="entryBabyname">Guess Name:</label>
          <input type="text" id="entryBabyname" class="form-control" v-model="newEntry.babyname">
        </div>
        <input type="submit" class="btn btn-primary" value="Add Entry">
      </form>
    </div>
  </div>
  <div class="panel panel-default">
    <div class="panel-heading">
      <h3 class="panel-title">Entries</h3>
      </div>
  <div class="panel-body">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Name</th>
          <th>Girl or Boy</th>
          <th>Date</th>
          <th>Weight</th>
          <th>Baby's Name</th>
          <th></th>
         </tr>
        </thead>
        <tbody>
          <tr v-for="entry in entries">
            <td>{{entry.contestant}}</td>
            <td>{{entry.gender}}</td>
            <td>{{entry.date}}</td>
            <td>{{entry.weight}}</td>
            <td>{{entry.babyname}}</td>
            <td><span class="glyphicon glyphicon-trash" aria-hidden="true" v-on:click="removeEntry(entry)"></span></td>
          </tr>
        </tbody>
    </table>
    </div>
  </div>
  </div>
</template>
<script>
import Firebase from 'firebase'
import toastr from 'toastr'
 let config = {
    apiKey: "AIzaSyCA7bgqjV6zRApbkdW6ajRWD3nNX06vifw",
    authDomain: "starter-project-13ba9.firebaseapp.com",
    databaseURL: "https://starter-project-13ba9.firebaseio.com",
    projectId: "starter-project-13ba9",
    storageBucket: "starter-project-13ba9.appspot.com",
    messagingSenderId: "508138870539"
  };
  
let app = Firebase.initializeApp(config)
let db = app.database()
let entriesRef = db.ref('entries')

export default {
  name: 'app',
  firebase: {
    entries: entriesRef
  },
  
  data () {
    return {
      newEntry: {
          contestant: '',
          gender: '',
          date: '',
          weight:'',
          babyname:''
    }
  }
  },
  
methods: {
  addEntry: function () {
    entriesRef.push(this.newEntry);
    this.newEntry.contestant = '';
    this.newEntry.gender = '';
    this.newEntry.date = '';
    this.newEntry.weight = '';
    this.newEntry.babyname = '';
  },
  removeEntry: function (entry) {
    entriesRef.child(entry['.key']).remove()
    toastr.success('Entry removed successfully')
  }
  }
}
  
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
</style>