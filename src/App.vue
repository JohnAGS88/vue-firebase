<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-primary">
      <a href="/" class="navbar-brand">PruebaFirebase</a>
    </nav>
    <div class="container">
      <div class="row mt-5">
        <div class="col-sm-4">
          <div class="card">
            <div class="card-header">
              <h3>Nueva Website</h3>
            </div>
          <div class="card-body">
            <form @submit.prevent="addWebsite">
          <div class="form-group">
            <input type="text" class="form-control" v-model="newWebsite.name" placeholder="Name">
          </div>
          <div class="form-group">
            <input type="text" class="form-control" v-model="newWebsite.author" placeholder="Author">
          </div>
          <div class="form-group">
            <input type="text" class="form-control" v-model="newWebsite.nurl" placeholder="URL">
          </div>
            <button type="submit" class="btn btn-primary">
              Save
            </button>
        </form>
      </div>
    </div>
  </div>
        <div class="col-sm-8 text-center">
          <div class="card">
            <div class="card-header">
              <h3>Lista de Webs</h3>
            </div>
            <div class="card-body">
              <table class="table table-striped table-bordered">
                <thead>
                  <tr>
                    <th>Nombre</th>
                    <th>Author</th>
                    <th>Operaciones</th>
                  </tr>
                </thead>
                <tbody>
                  
                </tbody>
              </table>
            </div>

          </div>
        </div>

      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
import Firebase from 'firebase';
import config from './config';

let app = Firebase.initializeApp(config);
let db = app.database();
let websitesRef = db.ref('websites');


export default {
  name: 'App',
    firebase: {
      websites: websitesRef
    },
    data() {
      return {
        newWebsite: {
          name: '',
          author: '',
          url: ''
        }
      }
    },
    methods: {
      addWebsite() {
        websitesRef.push(this.newWebsite);
        this.newWebsite.name = '';
        this.newWebsite.author = '';
        this.newWebsite.url = '';
      }
    }
}
</script>


