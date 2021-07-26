<template>
  <form>
    <div class="form-group">
      <label for="Id">ID</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput"
        placeholder="Enter ID"
        v-model="usersModal.id"
      />
    </div>
    <div class="form-group">
      <label for="photo">Photo</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput2"
        placeholder="Enter Photo"
        v-model="usersModal.Photo"
      />
    </div>
    <div class="form-group">
      <label for="photo">Name</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput2"
        placeholder="Enter Name"
        v-model="usersModal.Name"
      />
    </div>
    <div class="form-group">
      <label for="photo">Date</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput2"
        placeholder="Enter Date"
        v-model="usersModal.Date"
      />
    </div>
    <div class="btn btn-primary" @click="saveModal()">Save</div>
  </form>
</template>

<script>
export default {
  name: 'UsersModal',
  props:{
    itemEdit: {
      type: Object,
      default: null
    }
  },
  watch:{
    itemEdit(){
      if(this.itemEdit){
        this.usersModal = Object.assign({}, this.itemEdit)
      }else{
        this.usersModal = {}
      }
    }
  },
  data() {
    return {
      usersModal: {
        id: '',
        Photo: '',
        Name: '',
        Date: '',
      },
    }
  },
  methods: {
    saveModal() {
      this.$emit('save', this.usersModal)
      this.usersModal = {
        id: '',
        Photo: '',
        Name: '',
        Date: '',
      }
    },
  },
}
</script>