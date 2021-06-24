<template>
  <div class="container">
    <form @submit.prevent="onSubmitForm()">
      <div class="form-group">
        <label>First Name</label>
        <input
          type="text"
          class="form-control"
          name="firstName"
          id="firstName"
          v-model="firstName"
          @blur="validateInput"
        />
        <span class="error" v-if="!isValidInput">Please enter First Name</span>
      </div>
      <div class="form-group">
        <label>Last Name</label>
        <input
          type="text"
          class="form-control"
          name="lastName"
          id="lastName"
          v-model="lastName"
          @blur="validateInput"
        />
        <span class="error" v-if="!isValidInput">Please enter Last Name</span>
      </div>
      <div class="form-group">
        <label>Phone Number</label>
        <input
          type="text"
          class="form-control"
          name="phoneNumber"
          id="phoneNumber"
          v-model="phoneNumber"
          @blur="validateInput"
        />
        <span class="error" v-if="!isValidInput"
          >Please enter Phone Number</span
        >
      </div>
      <div class="form-group">
        <label>Email Id</label>
        <input
          type="text"
          class="form-control"
          name="emailId"
          id="emailId"
          v-model="emailId"
          @blur="validateInput"
        />
        <span class="error" v-if="!isValidInput">Please enter Email Id</span>
      </div>
      <div class="form-group">
        <label>Gender</label>
        <select class="form-control" name="gender" id="gender" v-model="gender">
          <option value="">Select</option>
          <option value="Male">Male</option>
          <option value="Female">Female</option>
          <option value="Other">Other</option>
        </select>
      </div>
      <br />
      <button type="submit" class="btn btn-primary">Add User</button>
    </form>
  </div>
  <br />
  <br />
  <div class="container">
    <table class="table" v-if="listOfUsers.length > 0">
      <thead>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Phone Number</th>
        <th>Email Id</th>
        <th>Gender</th>
      </thead>
      <tr v-for="user in listOfUsers" :key="user.index">
        <td>{{ user.firstName }}</td>
        <td>{{ user.lastName }}</td>
        <td>{{ user.phoneNumber }}</td>
        <td>{{ user.emailId }}</td>
        <td>{{ user.gender }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      firstName: "",
      lastName: "",
      phoneNumber: "",
      emailId: "",
      isValidInput: true,
      listOfUsers: [],
    };
  },
  emits :['update-user-list'],
  methods: {
    validateInput() {
      console.log("validate");
      if (this.firstName === "") {
        this.isValidInput = false;
      } else if (this.lastName === "") {
        this.isValidInput = false;
      } else if (this.phoneNumber === "") {
        this.isValidInput = false;
      } else if (this.emailId === "") {
        this.isValidInput = false;
      } else {
        this.isValidInput = true;
      }
    },
    onSubmitForm() {
      this.listOfUsers.push({
        firstName: this.firstName,
        lastName: this.lastName,
        phoneNumber: this.phoneNumber,
        emailId: this.emailId,
        gender: this.gender,
      });
      this.clearFormData();
      console.log(this.listOfUsers);
    },
    clearFormData() {
      this.firstName = "";
      this.lastName = "";
      this.phoneNumber = "";
      this.emailId = "";
      this.gender = "";
    },
  },
};
</script>
<style scoped>
.error {
  color: red;
}
</style>
