<template>
  <div class="container">

<div class="row">
          <div class="col-12">
            <div class="card">
              <div class="card-header">
                <h3 class="card-title">User Table</h3>

                <div class="card-tools">
                  <button class="btn btn-success" data-toggle="modal" data-target="#addNew">
                    add new
                    <i class="fa fa-user-plus"></i>
                  </button>
                  
                </div>
              </div>
              <!-- /.card-header -->
              <div class="card-body table-responsive p-0">
                <table class="table table-hover text-nowrap">
                  <thead>
                    <tr>
                      <th>ID</th>
                      <th>Name</th>
                      <th>Email</th>
                      <th>Type</th>
                      <th>registered At</th>
                      <th>Modify</th>
                    </tr>
                  </thead>
                  
                  <tbody>
                    <tr v-for="user in users" :key='user.id'>
                      <td>{{ user.id }}</td>
                      <td>{{ user.name | uptext }}</td>
                      <td>{{ user.email }}</td>
                      <td>{{ user.type }}</td>
                      <td>{{ user.created_at }}</td>
                      <td>
                        <a href="#">
                          <i class="fa fa-edit indigo"></i>
                        </a>
                        |
                        <a href="#">
                          <i class="fa fa-trash red"></i>
                        </a>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <!-- /.card-body -->
            </div>
            <!-- /.card -->
          </div>
        </div>



        <!-- Modal -->
      <div class="modal fade" id="addNew" tabindex="-1" role="dialog" aria-labelledby="addNewLabel" aria-hidden="true">
      <div class="modal-dialog" modal-dialog-centered role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="addNewLabel">Add New</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>


          <form @submit.prevent="createUser">
          <div class="modal-body">
            <!-- modal form input -->
            <div class="form-group">
              <input v-model="form.name" type="text" name="name" placeholder="name"
                class="form-control" :class="{ 'is-invalid': form.errors.has('name') }">
              <has-error :form="form" field="name"></has-error>
            </div>

            <div class="form-group">
              <input v-model="form.email" type="text" name="email" placeholder="email"
                class="form-control" :class="{ 'is-invalid': form.errors.has('email') }">
              <has-error :form="form" field="email"></has-error>
            </div>

            <div class="form-group">
              <input v-model="form.bio" name="bio" id="bio" placeholder="something about yourself"
                class="form-control" :class="{ 'is-invalid': form.errors.has('bio') }">
              <has-error :form="form" field="bio"></has-error>
            </div>

            <div class="form-group">
              <select name="type" v-model="form.type" id="type" placeholder="type"
                class="form-control" :class="{ 'is-invalid': form.errors.has('type') }">
                  <option>Select user role</option>
                  <option>Admin</option>
                  <option>Standard User </option>
                  <option>Author</option>
              </select>
              <has-error :form="form" field="type"></has-error>
            </div>

             <div class="form-group">
              <input v-model="form.password" name="password" id="password" placeholder="password"
                class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
              <has-error :form="form" field="password"></has-error>
            </div>

          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
            <button type="submit" class="btn btn-primary">Create</button>
          </div>

          </form>
        </div>
      </div>
      </div>
      <!-- Modal end-->

  </div>
</template>

<script>
    export default{
        data(){
          return{
            users: {},
            form:new Form({
              name:'',
              email: '',
              password:'',
              type:'',
              bio:'',
              photo:''
            })
          }
        },

        methods:{
          // this method loads the user from the data base
          loadUsers(){
            axios.get('api/user').then( ({data})=>(this.users = data.data) );
          },
          // the methods save the user 
          createUser(){
             this.form.post('api/user');
          }
        },
        created(){
            this.loadUsers();
            setInterval(() => this.loadUsers(),3000);
        }
    }
</script>