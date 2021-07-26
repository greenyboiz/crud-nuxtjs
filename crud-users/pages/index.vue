<template>
  <div class="container crud-users" style="margin-top: 50px">
    <div class="row flex-lg-nowrap">
      <div class="col">
        <div class="row flex-lg-nowrap">
          <div class="col mb-3">
            <div class="e-panel card">
              <div class="card-body">
                <div class="card-title">
                  <h6 class="mr-2">
                    <span>Users</span
                    ><small class="px-1">Be a wise leader</small>
                  </h6>
                </div>
                <div class="e-table">
                  <div class="table-responsive table-lg mt-3">
                    <table class="table table-bordered">
                      <thead>
                        <tr>
                          <th class="align-top">ID</th>
                          <th>Photo</th>
                          <th class="max-width">Name</th>
                          <th class="sortable">Date</th>
                          <th>Actions</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="(item, index) in users" :key="index">
                          <td class="align-middle">{{ item.id }}</td>
                          <td class="align-middle">{{ item.Photo }}</td>
                          <td class="text-nowrap align-middle">
                            {{ item.Name }}
                          </td>
                          <td class="text-nowrap align-middle">
                            <span>{{ item.Date }}</span>
                          </td>
                          <td class="align-middle">
                            <div class="btn-group align-top">
                              <button
                                class="btn btn-sm btn-outline-secondary badge"
                                type="button"
                                data-toggle="modal"
                                data-target="#myModal"
                                @click="editUser(item)"
                              >
                                Edit
                              </button>
                              <button
                                class="btn btn-sm btn-outline-secondary badge"
                                type="button"
                                @click="remove(index)"
                              >
                                <i class="fa fa-trash"></i>
                              </button>
                            </div>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-12 col-lg-3 mb-3">
            <div class="card">
              <div class="card-body">
                <div class="text-center px-xl-3">
                  <button
                    class="btn btn-success btn-block"
                    type="button"
                    data-toggle="modal"
                    data-target="#myModal"
                  >
                    New User
                  </button>
                </div>
                <hr class="my-3" />
              </div>
            </div>
          </div>
        </div>

        <!-- User Form Modal -->
        <div class="modal fade" id="myModal">
          <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
              <!-- Modal Header -->
              <div class="modal-header">
                <h4 class="modal-title">Add New User</h4>
                <button type="button" class="close" data-dismiss="modal">
                  &times;
                </button>
              </div>

              <!-- Modal body -->
              <div class="modal-body">
                <UsersModal :itemEdit="userEdit" @save="saveModal"></UsersModal>
              </div>

              <!-- Modal footer -->
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-dismiss="modal"
                >
                  Close
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import UsersModal from '../components/UsersModal.vue' 

export default {
  name: "crud-user",
  data() {
    return {
      users: [],
      userEdit: {}
    }
  },
  components:{
    UsersModal
  },
  mounted() {
    axios
      .get(
        'https://60efdfe2f587af00179d3b34.mockapi.io/api/crud-nuxt/crud-users'
      )
      .then((data) => {
        this.users = data.data
        console.log(this.users)
      })
  },
  methods: {
    remove(index) {
      if(confirm("Do you wanna delete this user?")){
        this.users.splice(index, 1)
      }
    },

    editUser(itemEdit){
      console.log(itemEdit)
      this.userEdit = itemEdit
    },

    saveModal(userItem){
      const index = this.users.findIndex((c) => c.id === userItem.id)
      console.log(index)
      if(index >= 0){
        this.users.splice(index, 1, userItem)
      }else{
        this.users.push(userItem)
      }
    }
  },
}
</script>

