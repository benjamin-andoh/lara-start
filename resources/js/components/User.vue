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
                      <th>Tpye</th>
                      <th>Modify</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>183</td>
                      <td>John Doe</td>
                      <td>11-7-2014</td>
                      <td><span class="tag tag-success">Approved</span></td>
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
            <button type="button" class="btn btn-primary">Create</button>
          </div>
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
        mounted(){
            console.log('Component mounted.')
        }
    }
</script>