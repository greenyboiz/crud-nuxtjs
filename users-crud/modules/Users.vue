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
                        <tr v-for="item in users" :key="item.id">
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
                                @click="editClick(item)"
                              >
                                Edit
                              </button>
                              <button
                                class="btn btn-sm btn-outline-secondary badge"
                                type="button"
                                @click="remove(item.id)"
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
                    @click="addClick()"
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
                <h4 class="modal-title">{{ modalTitle }}</h4>
                <button type="button" class="close" data-dismiss="modal">
                  &times;
                </button>
              </div>

              <!-- Modal body -->
              <div class="modal-body">
                <UsersModal />
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
import UsersModal from '../modules/UsersModal.vue'

export default {
  name: 'crud-user',
  data() {
    return {
      isEdit: false,
      users: [],
      modalTitle: '',
      userId: '',
      userPhoto: '',
      userName: '',
      userDate: '',
    }
  },

  components: {
      UsersModal
  },

  mounted() {
    this.getUsers()
  },
  methods: {
    getUsers() {
      axios
        .get(
          'https://60efdfe2f587af00179d3b34.mockapi.io/api/crud-nuxt/crud-users/'
        )
        .then((data) => {
          this.users = data.data
          console.log(this.users)
        })
    },

    addClick() {
      this.isEdit = false
      this.modalTitle = 'Add Users'
      this.userId = ''
      this.userPhoto = ''
      this.userName = ''
      this.userDate = ''
    },

    editClick(item) {
      this.isEdit = true
      this.modalTitle = 'Edit Users'
      this.userId = item.id
      this.userPhoto = item.Photo
      this.userName = item.Name
      this.userDate = item.Date
    },

    createUsers() {
      axios
        .post(
          'https://60efdfe2f587af00179d3b34.mockapi.io/api/crud-nuxt/crud-users/',
          {
            id: this.userId,
            Photo: this.userPhoto,
            Name: this.userName,
            Date: this.userDate,
          }
        )
        .then(() => {
          this.getUsers()
        })
    },

    updateUsers(id) {
      axios
        .put(
          'https://60efdfe2f587af00179d3b34.mockapi.io/api/crud-nuxt/crud-users/' +
            id,
          {
            Photo: this.userPhoto,
            Name: this.userName,
            Date: this.userDate,
          }
        )
        .then(() => {
          this.getUsers()
        })
    },

    remove(index) {
      if (confirm('Do you wanna delete this user?')) {
        axios
          .delete(
            'https://60efdfe2f587af00179d3b34.mockapi.io/api/crud-nuxt/crud-users/' +
              index
          )
          .then(() => {
            this.getUsers()
          })
      }
    },
  },
}
</script>

