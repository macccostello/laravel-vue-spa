<template>
<div>
  <div class="card table-card ">
  <div class="card-header d-flex align-items-center justify-content-between">
   <span> Users</span>
   <div class="d-flex">
    <form action="" class="mr-15">
      <div class="search-input">
        <i class='bx bx-search'></i>
        <input type="text" v-model="tableData.search" class="form-control" placeholder="Search"  @input="getUsers()"  >
      </div>
    </form>
     <div class="select mr-15">
        <select v-model="tableData.length" @change="getUsers()" class="custom-select">
            <option v-for="(records, index) in perPage" :key="index" :value="records">{{records}}</option>
        </select>
    </div>

     <button type="button" class="btn btn-success"  @click="newUserModal">Add User</button>
    </div>

  </div>
  <div class="card-body">
    <div class="is-loading" v-if="isLoading">
      <div class="spinner-border" role="status">
        <span class="sr-only">Loading...</span>
      </div>
    </div>

    {{selected}}
    <alert-success :form="form" :message="'User Added Successfully'" />
      <datatable :columns="columns" :sortKey="sortKey" :sortOrders="sortOrders" @sort="sortBy" @checkAll="checkAll">

            <tbody>
                <tr v-for="user in users" :key="user.id">
                  <td class="text-center">
                    <div class="custom-control custom-checkbox">
                      <input type="checkbox" class="custom-control-input" :value="user.id" v-model="selected" :id="user.id">
                      <label class="custom-control-label" :for="user.id"></label>
                    </div>
                  </td>
                    <td>
                      <a href="" class="table-avatar">
                        <span class="avatar">
                          <span>{{user.name.charAt(0)}}</span>
                        </span>
                          {{user.name}}
                      </a>
                      </td>
                    <td>{{user.email}}</td>
                    <td>{{user.phone}}</td>
                    <td>{{user.status}}</td>
                    <td>{{user.updated_at}}</td>
                    <td class="pl-4">
                      <a href="#!" @click="editUserModal(user)" class="btn btn-sm btn-edit"><i class='bx bxs-pencil' ></i></a>
                    </td>
                </tr>
            </tbody>
        </datatable>
        <pagination :pagination="pagination"
                  @prev="getUsers(pagination.prevPageUrl)"
                  @next="getUsers(pagination.nextPageUrl)">
        </pagination>
  </div>
</div>


<!-- Modal -->
<div class="modal modal-right fade" id="UserModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalScrollableTitle" aria-hidden="true">
  <div class="modal-dialog modal-dialog-scrollable" role="document">
    <div class="modal-content">
  <!-- <form @submit.prevent="storeUser" @keydown="form.onKeydown($event)"> -->
  <form  @submit.prevent="editUser ? updateUser() : storeUser()"  @keydown="form.onKeydown($event)">
      <div class="modal-header">
        <h5 v-show="!editUser" class="modal-title" >New User</h5>
        <h5  v-show="editUser" class="modal-title" >Update User</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">

        <!-- <p>An image of the person, it's best if it has the same length and height</p> -->
        <div class="form-group">
          <div class="media align-items-center">
            <img src="/images/avatar.jpg" v-if="!image" class="mr-3" style="height:50px;width:50px;object-fit:cover;border-radius:50px" alt="...">
            <img v-else :src="image" style="height:50px;width:50px;object-fit:cover;border-radius:50px" class="mr-3" />
            <div class="media-body">
              <div v-if="!image">
                <p style="margin-bottom: 3px;font-size: 15px;">Select an image</p>
                <input type="file" @change="onFileChange">
              </div>
               <div v-else>
                 <a href="" @click.prevent="removeImage">Remove image</a>
              </div>
            </div>
          </div>
        </div>
        <div class="form-group">
        <label>Name</label>
          <input v-model="form.name" :class="{ 'is-invalid': form.errors.has('name') }" class="form-control" type="text" name="name" placeholder="John Deo">
          <has-error :form="form" field="name" />
        </div>
        <div class="form-group">
          <label>Email</label>
          <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" name="email" type="email" class="form-control"  placeholder="john@example.com">
          <has-error :form="form" field="email" />
        </div>
        <div class="form-group">
          <label>Phone</label>
          <input v-model="form.phone" :class="{ 'is-invalid': form.errors.has('phone') }" name="phone" type="text" class="form-control"  placeholder="Mobile Number">
          <has-error :form="form" field="phone" />
        </div>
          <div class="form-group">
          <label>Password</label>
          <input v-model="form.password" :class="{ 'is-invalid': form.errors.has('password') }" name="password" type="password" class="form-control"  placeholder="+6 Characters">
           <has-error :form="form" field="password" />
        </div>
        <div class="form-group">
          <label>Status</label>
          <select class="custom-select" v-model="form.status">
            <option value="1">Active</option>
            <option value="0">Deactive</option>
          </select>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-light" data-dismiss="modal">Close</button>
        <v-button v-show="!editUser" :loading="form.busy" type="success">Save User</v-button>
        <v-button v-show="editUser" :loading="form.busy" type="success">Update User</v-button>
      </div>
      </form>
    </div>
  </div>
</div>
</div>
</template>

<script>
import Datatable from '~/components/Datatable.vue';
import Pagination from '~/components/Pagination.vue';
import Form from 'vform';

const axios = require('axios');
export default {
    components: { datatable: Datatable, pagination: Pagination },
    created() {
        this.getUsers();
    },
    data() {
        let sortOrders = {};
        let columns = [
            { label: 'Name', name: 'name' },
            { label: 'Email', name: 'email'},
            { label: 'Phone', name: 'phone'},
            { label: 'Status', name: 'status'},
            { label: 'Created At', name: 'updated_at'},
            { label: 'Actions', name: 'action'}
        ];
        columns.forEach((column) => {
           sortOrders[column.name] = -1;
        });
        return {
           editUser: false,
           isLoading:false,
            image: '',
            users: [],
            columns: columns,
            sortKey: 'name',
            sortOrders: sortOrders,
            perPage: ['10', '20', '30'],
            selected: [],
	         	selectAll: false,
            tableData: {
                draw: 0,
                length: 10,
                search: '',
                column: 0,
                dir: 'desc',
            },
            pagination: {
                lastPage: '',
                currentPage: '',
                total: '',
                lastPageUrl: '',
                nextPageUrl: '',
                prevPageUrl: '',
                from: '',
                to: ''
            },
            form: new Form({
              id:'',
              name: '',
              email: '',
              phone: '',
              password: '',
              status: '',
          }),
        }
    },
    methods: {
       editUserModal(user){
           this.editUser = true;
            this.form.reset();
            $('#UserModal').modal('show');
            this.form.fill(user);
        },
        newUserModal(){
            this.editUser = false;
            this.form.reset();
            $('#UserModal').modal('show');
        },
        async storeUser () {
          await this.form.post('/api/getUsers')
          this.getUsers();
          this.form.reset();
          $('#UserModal').modal('hide');
        },
         async updateUser () {
           await this.form.post('/api/updateUser')
                .then(() => {
                    // success
                  $('#UserModal').modal('hide');
                   this.getUsers();
                })
                .catch(() => {
                   console.log('failed');
                });
        },

        getUsers(url = '/api/getUsers') {
             this.isLoading =true;
            this.tableData.draw++;
            axios.get(url, {params: this.tableData})
                .then(response => {
                    let data = response.data;
                    if (this.tableData.draw == data.draw) {
                        this.users = data.data.data;
                        this.configPagination(data.data);
                    }
                     this.isLoading =false;
                })
                .catch(errors => {
                    console.log(errors);
                });
        },
        configPagination(data) {
            this.pagination.lastPage = data.last_page;
            this.pagination.currentPage = data.current_page;
            this.pagination.total = data.total;
            this.pagination.lastPageUrl = data.last_page_url;
            this.pagination.nextPageUrl = data.next_page_url;
            this.pagination.prevPageUrl = data.prev_page_url;
            this.pagination.from = data.from;
            this.pagination.to = data.to;
        },
        sortBy(key) {
            this.sortKey = key;
            this.sortOrders[key] = this.sortOrders[key] * -1;
            this.tableData.column = this.getIndex(this.columns, 'name', key);
            this.tableData.dir = this.sortOrders[key] === 1 ? 'asc' : 'desc';
            this.getUsers();
        },
        getIndex(array, key, value) {
            return array.findIndex(i => i[key] == value)
        },
        onFileChange(e) {
          var files = e.target.files || e.dataTransfer.files;
          if (!files.length)
            return;
          this.createImage(files[0]);
        },
        createImage(file) {
          var image = new Image();
          var reader = new FileReader();
          var vm = this;

          reader.onload = (e) => {
            vm.image = e.target.result;
          };
          reader.readAsDataURL(file);
        },
        removeImage: function (e) {
          this.image = '';
        },
        checkAll() {

          this.selected = [];
          if (!this.selectAll) {
            for (let i in this.users) {
              this.selected.push(this.users[i].id);
            }
          }
             this.selectAll = !this.selectAll;
        }

    }
};
</script>
