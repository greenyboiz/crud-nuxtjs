<template>
  <form>
    <div class="form-group">
      <label for="Id">ID</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput"
        placeholder="Enter ID"
        v-model="userId"
      />
    </div>
    <div class="form-group">
      <label for="photo">Photo</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput2"
        placeholder="Enter Photo"
        v-model="userPhoto"
      />
    </div>
    <div class="form-group">
      <label for="photo">Name</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput2"
        placeholder="Enter Name"
        v-model="userName"
      />
    </div>
    <div class="form-group">
      <label for="photo">Date</label>
      <input
        type="text"
        class="form-control"
        id="formGroupExampleInput2"
        placeholder="Enter Date"
        v-model="userDate"
      />
    </div>
    <div
      class="btn btn-primary"
      v-if="!isEdit"
      @click="createUsers()"
      data-dismiss="modal"
    >
      Add
    </div>
    <div
      class="btn btn-primary"
      v-if="isEdit"
      @click="updateUsers(userId)"
      data-dismiss="modal"
    >
      Update
    </div>
  </form>
</template>