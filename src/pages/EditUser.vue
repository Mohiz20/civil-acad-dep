<template>
  <div class="create-user">
    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-body">
            <div class="row">
              <div class="col-12">
                <h5><strong>Update User</strong></h5>
                <span class="back" @click="move('/users')"
                  ><i class="fa fa-user"></i>
                  <strong class="back">Users</strong></span
                >
                <i class="fa fa-chevron-right"></i><strong>Update User</strong>
              </div>
            </div>
            <div class="row mt-5 mx-md-3">
              <div class="col-12 ">
                                <label for="first_name"><strong>Upload Image</strong></label> <br>
                                <input type="file" class="btn btn-primary" accept="image/*"  @change="uploadImage" ref="AvatarInput">
                            </div>         
              <div class="col-12">
                <form @submit.prevent>
                  <div class="row">
                    <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                      <div class="form-group">
                        <label for="first_name"
                          ><strong>First Name*</strong></label
                        >
                        <input
                          type="text"
                          class="form-control"
                          v-model="user.first_name"
                          placeholder="Enter First Name"
                          required
                        />
                      </div>
                    </div>
                    <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                      <div class="form-group">
                        <label for="last_name"
                          ><strong>Last Name*</strong></label
                        >
                        <input
                          type="text"
                          class="form-control"
                          v-model="user.last_name"
                          placeholder="Enter Last Name"
                          required
                        />
                      </div>
                    </div>
                    <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                      <div class="form-group">
                        <label for="email"><strong>Email*</strong></label>
                        <input
                          type="email"
                          class="form-control"
                          v-model="user.email"
                          placeholder="Enter Email"
                          required
                        />
                      </div>
                    </div>
                    <!-- <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                      <div class="form-group">
                        <label for="password"><strong>Password*</strong></label>
                        <input
                          type="text"
                          class="form-control"
                          placeholder="Enter Password"
                          required
                          v-model="user.password"
                        />
                      </div>
                    </div> -->
                     <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                      <div class="form-group">
                        <label for="job_title"><strong>Country*</strong></label>
                        <select
                          class="form-control"
                          v-model="user.country"
                          required
                        >
                        <option :value="item.name" v-for="(item, index) in countries" :key="index">{{item.name}}</option>
                        </select>
                      </div>
                    </div>
                    <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                      <div class="form-group">
                        <label for="mobile"><strong>Phone*</strong></label>
                        <div class="row">
                          <div class="col-4">
                            <select
                                class="form-control"
                                v-model="user.country"
                                required
                                disabled
                              >
                                <option :value="item.name" v-for="(item, index) in countries" :key="index">{{item.dial_code}}</option>
                            </select> 
                          </div>
                          <div class="col-8">
                            <input
                              type="text"
                              class="form-control"
                              v-model="user.phone"
                              maxlength="10"
                              pattern="[1-9]{1}[0-9]{9}"
                              @keypress="phoneno"
                              placeholder="Enter Phone"
                              required
                            />
                          </div> 
                          </div>
                        </div>
                    </div>
                    <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                      <div class="form-group">
                        <label for="gender"><strong>Gender*</strong></label>
                        <select
                          class="form-control"
                          v-model="user.gender"
                          required
                        >
                          <option value="male">Male</option>
                          <option value="female">Female</option>
                          <option value="other">Other</option>
                        </select>
                      </div>
                    </div>
                    <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                        <div class="form-group">
                            <label for="job_title"><strong>Residence*</strong></label>
                            <input type="text" class="form-control" v-model="user.residence" placeholder="Enter Residence" required>
                        </div>
                    </div>
                    <div class="col-12 mt-3 text-right">
                      <button class="btn btn-primary" @click="updateUser()">
                        Update User
                      </button>
                    </div>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-body">
            <div class="row">
              <div class="col-12">
                <h5><strong>Reset Password</strong></h5>
              </div>
            </div>
            <form @submit.prevent>
              <div class="row mt-3 mx-md-3">
                <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                  <div class="form-group">
                    <label for="current-password"
                      ><strong>Current Password*</strong></label
                    >
                    <input
                      :type="showCurrentPassword?'text':'password'"
                      class="form-control"
                      placeholder="Enter Current Password"
                      v-model="currentPassword"
                      required
                    />
                    <span class="visiblePass"><i :class="showCurrentPassword?'fa fa-eye':'fa fa-eye-slash'" @click="showCurrentPassword=!showCurrentPassword;"></i></span>
                  </div>
                </div>
                <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                  <div class="form-group">
                    <label for="new-password"
                      ><strong>New Password*</strong></label
                    >
                    <input
                      :type="showNewPassword?'text':'password'"
                      class="form-control"
                      placeholder="Enter New Password"
                      v-model="newPassword"
                      required
                    />
                    <span class="visiblePass"><i :class="showNewPassword?'fa fa-eye':'fa fa-eye-slash'" @click="showNewPassword=!showNewPassword;"></i></span>
                  </div>
                </div>
                <div class="col-12 col-md-6 col-lg-6 col-xl-4 mt-2">
                  <div class="form-group">
                    <label for="confirm-password"
                      ><strong>Confirm Password*</strong></label
                    >
                    <input
                      :type="showConfirmPassword?'text':'password'"
                      class="form-control"
                      placeholder="Confirm Password"
                      v-model="cPassword"
                      required
                    />
                    <span class="visiblePass"><i :class="showConfirmPassword?'fa fa-eye':'fa fa-eye-slash'" @click="showConfirmPassword=!showConfirmPassword;"></i></span>
                  </div>
                </div>
                <div class="col-12 mt-2 text-right">
                  <div class="form-group">
                    <button class="btn btn-primary" @click="resetPassword()">
                      Reset Password
                    </button>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import countries from '../assets/countries.json'
export default {
  name: "EditUser",
  created() {
    this.getUserDetails(this.$route.params.id);
  },
  methods: {
    phoneno(e){
            let a = [];
            let k = e.which;
            let i;
            for (i = 48; i < 58; i++)
                a.push(i);

            if (!(a.indexOf(k)>=0))
                e.preventDefault();
    },
    updateUser() {
      console.log("updating user");
      let newUser = new FormData();
      newUser.append("first_name", this.user.first_name);
      newUser.append("last_name", this.user.last_name);
      newUser.append("email", this.user.email);
      newUser.append("phone", Number(this.user.phone));
      newUser.append("gender", this.user.gender);
      newUser.append("residence", this.user.residence);
      newUser.append("country", this.user.country);
      newUser.append("nationality", this.user.country);
        newUser.append("image", this.image);
      console.log(newUser);
      axios
        .post(
          this.APIServer + "admin/user/update-user/" + this.$route.params.id,
          newUser,
          {
            headers: { Authorization: this.$store.state.token },
          }
        )
        .then((response) => {
          if (response.data.status == "success") {
            this.$router.push({ path: "/users" });
            this.openNotificationWithIcon(
              "success",
              "User updated successfully",
              "bottomRight"
            );
          } else {
            if(response.data.message==="User updated successfully!"){
              this.$router.push({ path: "/users" });
              this.openNotificationWithIcon(
                "success",
                "User updated successfully",
                "bottomRight"
              );
            }
            else{
                this.openNotificationWithIcon(
                  "warning",
                  response.data.message,
                  "bottomRight"
                );
            }
          }
          console.log(response.data);
        })
        .catch((e) => {
          console.log("API failed");
          console.log(e);
          this.openNotificationWithIcon(
            "error",
            response.data.message,
            "bottomRight"
          );
        });
    },
    uploadImage(event) {
      let file = event.target.files[0];
      if (file) {
        const url = "https://api.cloudinary.com/v1_1/dz5fltj9r/image/upload";
        const data = new FormData();
        data.append("file", file);
        data.append("upload_preset", "hammad");
        axios
          .post(url, data)
          .then((response) => {
            console.log(response.data);
            this.image = response.data.secure_url;
            this.openNotificationWithIcon(
              "success",
              "Image uploaded to cloudinary",
              "bottomRight"
            );
          })
          .catch((e) => {
            console.log("API failed");
            console.log(e);
            this.openNotificationWithIcon(
              "error",
              "Image upload failed",
              "bottomRight"
            );
          });
      }
    },
    resetPassword() {
      axios
        .post(
          this.APIServer +
            "admin/user/update-password/" +
            this.$route.params.id,
          {
            current_password: this.currentPassword,
            password: this.newPassword,
            c_password: this.cPassword,
          },
          {
            headers: { Authorization: this.$store.state.token },
          }
        )
        .then((response) => {
          if (response.data.message != null) {
            if(response.data.message === "password do not match"){
              this.openNotificationWithIcon(
                  "error",
                  response.data.message,
                  "bottomRight"
              );
            }
            if(response.data.message === "The given data was invalid."){
              if(response.data.errors.current_password && response.data.errors.current_password.length>0){
                this.openNotificationWithIcon(
                  "error",
                  response.data.errors.current_password[0],
                  "bottomRight"
                );
              }
              if(response.data.errors.c_password && response.data.errors.c_password.length>0){
                this.openNotificationWithIcon(
                  "error",
                  response.data.errors.c_password[0],
                  "bottomRight"
                );
              }
              if(response.data.errors.password && response.data.errors.password.length>0){
                this.openNotificationWithIcon(
                  "error",
                  response.data.errors.password[0],
                  "bottomRight"
                );
              }
            }
            if(response.data.message === "Password changed successfully!"){
                this.openNotificationWithIcon(
                  "success",
                  response.data.message,
                  "bottomRight"
                );
                this.$router.push({ path: "/users" });
            }
            // if(response.data.errors && response.data.errors.password
            //  && response.data.errors.password.length > 0){
            //     this.openNotificationWithIcon(
            //       "error",
            //       response.data.errors.password[0],
            //       "bottomRight"
            //     );
            // }
            // else{
            //     this.openNotificationWithIcon(
            //       "success",
            //       response.data.message,
            //       "bottomRight"
            //     );
            // }
          }
        })
        .catch((e) => {
          console.log("API failed");
          this.openNotificationWithIcon(
            "error",
            "Internal server error",
            "bottomRight"
          );
        });
    },
    getUserDetails(id) {
      axios
        .get(this.APIServer + "admin/user/show/" + id, {
          headers: { Authorization: this.$store.state.token },
        })
        .then((response) => {
          if (response.data.status == "success") {
            this.user = response.data.data;
            // console.log("user updated");
          }
        })
        .catch((e) => {
          console.log("API failed");
          console.log(e);
        });
    },
    openNotificationWithIcon(type, message, place) {
      this.$notification[type]({
        message: "Response",
        description: message,
        place,
      });
    },
    move(to) {
      this.$router.push({ path: to });
    },
    pickAvatar() {
      this.$refs.AvatarInput.click();
    },
    onAvatarSelected(event) {
      let file = event.target.files[0];
      if (file) {
        this.image = URL.createObjectURL(file);
      }
    },
  },
  data() {
    return {
      countries: countries,
      showNewPassword:false,
      showConfirmPassword:false,
      showCurrentPassword: false,
      image: null,
      APIServer: process.env.VUE_APP_SERVER_ADDRESS,
      currentPassword: null,
      newPassword: null,
      cPassword: null,
      //   user: null,
      user: {
        first_name: null,
        last_name: null,
        email: null,
        country: null,
        phone: null,
        nationality: null,
        gender: null,
      },
    };
  },
};
</script>

<style scoped>
</style>