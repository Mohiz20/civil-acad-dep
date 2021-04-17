<template>
  <div class="contact">
    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-body">
            <form @submit.prevent>
              <div class="row">
                <div class="col-12">
                  <h5><strong>About Page Details</strong></h5>
                  <hr />
                </div>
                <div class="col-12 my-3">
                  <h5><strong>Company Profile</strong></h5>
                  <div class="form-group mt-4">
                    <label><strong>Upload Images</strong></label> <br />
                    <input
                      type="file"
                      @change="uploadImage($event, 'profile')"
                      multiple
                      class="btn btn-primary btn-sm"
                    />
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>English</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Heading*</strong></label
                      >
                      <input
                        type="text"
                        v-model="data.about_profile.title_en"
                        class="form-control"
                        placeholder="Enter English Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_profile.content_en"
                      ></vue-editor>
                    </div>
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>Arabic</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Heading*</strong></label
                      >
                      <input
                        type="text"
                        v-model="data.about_profile.title_ar"
                        class="form-control"
                        placeholder="Enter Arabic Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_profile.content_ar"
                      ></vue-editor>
                    </div>
                  </div>
                </div>

                <div class="col-12 my-3">
                  <h5><strong>Our Mission</strong></h5>
                  <div class="form-group mt-4">
                    <label><strong>Upload Images</strong></label> <br />
                    <input
                      type="file"
                      @change="uploadImage($event, 'mission')"
                      multiple
                      class="btn btn-primary btn-sm"
                    />
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>English</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Heading*</strong></label
                      >
                      <input
                        type="text"
                        v-model="data.about_mission.title_en"
                        class="form-control"
                        placeholder="Enter English Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_mission.content_en"
                      ></vue-editor>
                    </div>
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>Arabic</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Heading*</strong></label
                      >
                      <input
                        type="text"
                        v-model="data.about_mission.title_ar"
                        class="form-control"
                        placeholder="Enter Arabic Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_mission.content_ar"
                      ></vue-editor>
                    </div>
                  </div>
                </div>

                <div class="col-12 my-3">
                  <h5><strong>Our Vision</strong></h5>
                  <div class="form-group mt-4">
                    <label><strong>Upload Images</strong></label> <br />
                    <input
                      type="file"
                      @change="uploadImage($event, 'vision')"
                      multiple
                      class="btn btn-primary btn-sm"
                    />
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>English</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Heading*</strong></label
                      >
                      <input
                        type="text"
                        v-model="data.about_vision.title_en"
                        class="form-control"
                        placeholder="Enter English Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_vision.content_en"
                      ></vue-editor>
                    </div>
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>Arabic</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Heading*</strong></label
                      >
                      <input
                        type="text"
                        class="form-control"
                        v-model="data.about_vision.title_ar"
                        placeholder="Enter Arabic Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_vision.content_ar"
                      ></vue-editor>
                    </div>
                  </div>
                </div>

                <!-- <div class="col-12 my-3">
                  <h5><strong>Accreditation &amp; Membership</strong></h5>
                  <div class="form-group mt-4">
                    <label><strong>Upload Images</strong></label> <br />
                    <input
                      type="file"
                      multiple
                      class="btn btn-primary btn-sm"
                    />
                  </div>
                </div> -->

                <div class="col-12 my-3">
                  <h5><strong>Our Clients</strong></h5>
                  <div class="form-group mt-4">
                    <label><strong>Upload Images</strong></label> <br />
                    <input
                      type="file"
                      @change="uploadImage($event, 'client')"
                      multiple
                      class="btn btn-primary btn-sm"
                    />
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>English</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Heading*</strong></label
                      >
                      <input
                        type="text"
                        v-model="data.about_client.title_en"
                        class="form-control"
                        placeholder="Enter English Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>English Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_client.content_en"
                      ></vue-editor>
                    </div>
                  </div>
                </div>
                <div class="col-12 col-md-12 col-lg-12 col-xl-6">
                  <div class="content-area">
                    <h5 class="text-center"><strong>Arabic</strong></h5>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Heading*</strong></label
                      >
                      <input
                        type="text"
                        v-model="data.about_client.title_ar"
                        class="form-control"
                        placeholder="Enter Arabic Heading"
                        required
                      />
                    </div>
                    <div class="form-group">
                      <label for="title"
                        ><strong>Arabic Content*</strong></label
                      >
                      <vue-editor
                        v-model="data.about_client.content_ar"
                      ></vue-editor>
                    </div>
                  </div>
                </div>

                <div class="col-12 text-right mt-3">
                  <button class="btn btn-primary" @click="saveAboutData()">
                    Save Information
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>

    <b-modal v-model="viewModal" hide-footer title="Contact Detials">
      <div class="row">
        <div class="col-6">
          <div class="form-group">
            <label for=""><strong>Name</strong></label>
            <p>Arslan</p>
          </div>
        </div>
        <div class="col-6">
          <div class="form-group">
            <label for=""><strong>Email</strong></label>
            <p>arslan@gmail.com</p>
          </div>
        </div>
        <div class="col-6">
          <div class="form-group">
            <label for=""><strong>Message</strong></label>
            <p>Hello</p>
          </div>
        </div>
      </div>
    </b-modal>
  </div>
</template>

<script>
import { VueEditor } from "vue2-editor";
import axios from "axios";
export default {
  name: "users",
  components: {
    VueEditor,
  },
  computed: {
    rows() {
      return this.items.length;
    },
  },
  data() {
    return {
      APIServer: process.env.VUE_APP_SERVER_ADDRESS,
      mainProps: { blank: false, blankColor: "#777", width: 80, height: 80 },
      mainProps1: { blank: false, blankColor: "#777", width: 30, height: 30 },
      editUser: null,
      image: null,
      editModal: false,
      createModal: false,
      viewModal: false,
      pagination: {},
      loading: false,
      visible: false,
      user: {
        first_name: null,
        last_name: null,
        email: null,
        mobile: null,
        nationality: null,
        image: null,
        job_title: null,
        isUploaded: false,
        status: "active",
      },
      data: {
        about_client: {
          content_ar: null,
          content_en: null,
          title_ar: null,
          title_en: null,
          images: [],
        },
        about_mission: {
          content_ar: null,
          content_en: null,
          title_ar: null,
          title_en: null,
          images: [],
        },
        about_profile: {
          content_ar: null,
          content_en: null,
          title_ar: null,
          title_en: null,
          images: [],
        },
        about_vision: {
          content_ar: null,
          content_en: null,
          title_ar: null,
          title_en: null,
          images: [],
        },
      },
      columns: [
        {
          title: "ID",
          dataIndex: "key",
          sorter: (a, b) => a.key - b.key,
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Name",
          dataIndex: "name",
          sorter: (a, b) => a.name.length - b.name.length,
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Email",
          dataIndex: "email",
          sorter: (a, b) => a.email.length - b.email.length,
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Message",
          dataIndex: "message",
          sorter: (a, b) => a.message.length - b.message.length,
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Created At",
          dataIndex: "created_at",
          sorter: (a, b) => a.created_at.length - b.created_at.length,
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Actions",
          scopedSlots: { customRender: "actions" },
        },
      ],
    };
  },
  created() {
    this.getAboutData();
  },
  methods: {
    getAboutData() {
      axios
        .get(this.APIServer + "front/about/setting", {
          headers: { Authorization: this.$store.state.token },
        })
        .then((response) => {
          console.log(response.data);
          this.data.about_client = response.data.data[3];
          this.data.about_client.images =[];
          this.data.about_mission = response.data.data[1];
          this.data.about_mission.images = [];
          this.data.about_profile = response.data.data[0];
          this.data.about_profile.images = [];
          this.data.about_vision = response.data.data[2];
          this.data.about_vision.images = [];
        });
    },
    saveAboutData() {
      if (this.isUploaded == true) {
        console.log("savimg about data");
        const data = {
            profile_image : this.data.about_profile.images,
            mission_image: this.data.about_mission.images,
            vision_image: this.data.about_vision.images,
            client_image: this.data.about_client.images,
            profile_title_en : this.data.about_profile.title_en,
            profile_title_ar : this.data.about_profile.title_ar,
            profile_content_en: this.data.about_profile.content_en,
            profile_content_ar: this.data.about_profile.content_ar,
            mission_title_en : this.data.about_mission.title_en,
            mission_title_ar : this.data.about_mission.title_ar,
            mission_content_en : this.data.about_mission.content_en,
            mission_content_ar : this.data.about_mission.content_ar,
            vision_title_en : this.data.about_vision.title_en,
            vision_title_ar : this.data.about_vision.title_ar,
            vision_content_en : this.data.about_vision.content_en,
            vision_content_ar : this.data.about_vision.content_ar,
            client_title_en : this.data.about_client.title_en,
            client_title_ar : this.data.about_client.title_ar,
            client_content_en : this.data.about_client.content_en,
            client_content_ar : this.data.about_client.content_ar
            }
        axios
          .post(this.APIServer + "front/about/setting/save", data)
          .then((response) => {
            console.log(response.data);
            this.openNotificationWithIcon(
              "success",
              response.data.data,
              "bottomRight"
            );
            this.getAboutData();
          })
          .catch((e) => {
            this.openNotificationWithIcon(
              "error",
              "Internal server error",
              "bottomRight"
            );
          });
      } else {
        this.openNotificationWithIcon(
          "warning",
          "All images are not selected or uploaded yet, please try again",
          "bottomRight"
        );
      }
    },
    uploadImage(event, type) {
      this.isUploaded = false;
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
            if (type == "profile")
              this.data.about_profile.images.push(response.data.secure_url);
            else if (type == "mission")
              this.data.about_mission.images.push(response.data.secure_url);
            else if (type == "vision")
              this.data.about_vision.images.push(response.data.secure_url);
            else if (type == "client")
              this.data.about_client.images.push(response.data.secure_url);
            console.log("type : " + type);
            this.isUploaded = true;
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
    move(to) {
      this.$router.push({ path: to });
    },
    openNotificationWithIcon(type, message, place) {
      this.$notification[type]({
        message: "Response",
        description: message,
        place,
      });
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
    createUser() {
      let last = this.data[this.data.length - 1];
      this.user.key = last.key + 1;
      this.data.push(this.user);
      this.viewModal = false;
    },
    edit(record) {
      this.editUser = record;
      this.editModal = true;
    },
    update() {
      this.editModal = false;
    },
    // view(record) {

    // },
    deleteItem(record) {
      let index = this.data.indexOf(record);
      if (index !== -1) {
        this.data.splice(index, 1);
      }
    },
    onChangeStatus(record) {
      let index = this.data.indexOf(record);
      if (index !== -1) {
        let status = this.data[index].status;
        if (status == "active") {
          this.data[index].status = "inactive";
        } else {
          this.data[index].status = "active";
        }
      }
    },
  },
};
</script>

<style scoped>
.content-area {
  border: 1px solid #eee;
  border-radius: 5px;
  padding: 20px 30px;
}
</style>