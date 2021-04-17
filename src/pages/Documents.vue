<template>
  <div class="site-settings">
    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-body">
            <div class="row">
              <div class="col-12">
                <h5><strong>Upload Documents</strong></h5>
              </div>
            </div>
            <div class="row mt-3">
              <div class="col-3 p-3">
                <label for=""><strong>Document Title</strong></label>
                <input
                  type="text"
                  v-model="data.title"
                  class="form-control"
                  placeholder="Title"
                />
              </div>
              <div class="col-12 p-3">
                <label for="upload"><strong>Upload Document</strong></label>
                <br />
                <input
                  type="file"
                  class="btn btn-primary"
                  @change="uploadImage"
                  ref="AvatarInput"
                />
              </div>
              <div class="col-12 col-md-12 text-right">
                <div class="form-group">
                  <button class="btn btn-primary" @click="saveDocuments()">
                    Save
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <div class="card">
          <div class="card-body">
            <div class="row">
              <div class="col-md-6 col-lg-6 col-xl-6 col-6 col-sm-6 col-xs-6">
                <h5><strong>Documents List</strong></h5>
              </div>
              <div
                class="col-md-6 col-lg-6 col-xl-6 col-6 col-sm-6 col-xs-6 text-right"
              >
                <b-dropdown
                  id="dropdown-left"
                  text="Download"
                  variant="primary"
                  class="m-2"
                >
                  <b-dropdown-item>CSV</b-dropdown-item>
                  <b-dropdown-item>PDF</b-dropdown-item>
                </b-dropdown>
              </div>
            </div>
            <div class="row my-3">
              <!-- <div class="col-12 col-md-3">
                <label for="filter"><strong>Filter By Status</strong></label>
                <select class="form-control">
                  <option :value="null">Filter Users By Status</option>
                  <option value="all">All</option>
                  <option value="1">Active</option>
                  <option value="0">Inactive</option>
                </select>
              </div>
              <div class="col-12 col-md-3 mt-md-0 mt-3">
                <label for="filter"
                  ><strong>Search By Name/Phone</strong></label
                >
                <input
                  type="text"
                  placeholder="Search By Name/Phone"
                  class="form-control"
                />
              </div> -->
              <div class="col-12 col-md-3 mt-md-0 mt-3">
                <label for="filter"><strong>Search By Title</strong></label>
                <input
                  type="text"
                  placeholder="Search By Title"
                  class="form-control"
                 />
              </div>
              <div class="col-12 col-md-3 mt-md-0 mt-3">
                <label for="filter"><strong>Search By Date</strong></label>
                <a-range-picker
                  class="date-input"
                  size="default"
                />
              </div>
            </div>
            <div class="row">
              <div class="col-md-12">
                <a-table
                  class="table"
                  :columns="columns"
                  :dataSource="documentList"
                  :scroll="{ x: 1300 }"
                  :loading="loading"
                >
                  <span slot="image" slot-scope="id, record">
                    <b-img v-bind="mainProps1" :src="record.image"></b-img>
                  </span>
                  <span slot="status" slot-scope="id, record">
                    <a-switch
                      :checked="getBoolVal(record.status)"
                      @change="onChangeStatus(record)"
                    />
                  </span>
                  <span slot="actions" slot-scope="id, record">
                    <i class="fa fa-eye" @click="viewUserData(record)"></i>
                    <i
                      class="fa fa-pencil"
                      @click="move('/edit-user/' + record.id)"
                    ></i>
                    <i
                      class="fa fa-trash"
                      @click="
                        deleteModal = true;
                        storeRecord = record;
                      "
                    ></i>
                  </span>
                </a-table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Documents",
  data() {
    return {
      APIServer: process.env.VUE_APP_SERVER_ADDRESS,
      data: {
        url: null,
        title: null,
      },
      columns: [
        {
          title: "Image",
          scopedSlots: { customRender: "image" },
        },
        {
          title: "Id",
          dataIndex: "id",
          sorter: (a, b, sortOrder) => a.id - b.id,
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Date",
          dataIndex: "created_at",
          sorter: (a, b) => {
            if(!a.created_at){
              a.created_at = '';
            }
            if(!b.created_at){
              b.created_at = '';
            }
            return  a.created_at.localeCompare(b.created_at);
          },
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Title",
          dataIndex: "title",
          sorter: (a, b, sortOrder) => a.title.localeCompare(b.title),
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Actions",
          scopedSlots: { customRender: "actions" },
        },
      ],
      documentList : [{
        id : 1,
        created_at: "1-1-2020",
        title : 'title',
        iamge : null
      }],
      trainerStatus: true,
      trainserSub: null,
      studentSub: null,
      studentStatus: true,
      adminComission: null,
      adminStatus: true,
      promotionCharge: null,
      promotionStatus: true,
    };
  },
  created() {
    // this.getSiteSettings();
  },
  methods: {
    uploadImage(event) {
      let file = event.target.files[0];
      if (file) {
        const url = "https://api.cloudinary.com/v1_1/dz5fltj9r/upload";
        const data = new FormData();
        data.append("file", file);
        data.append("upload_preset", "hammad");
        axios
          .post(url, data)
          .then((response) => {
            console.log(response.data);
            this.data.url = response.data.secure_url;
            this.openNotificationWithIcon(
              "success",
              "Document uploaded to cloudinary",
              "bottomRight"
            );
          })
          .catch((e) => {
            console.log("API failed");
            console.log(e);
            this.openNotificationWithIcon(
              "error",
              "Document upload failed",
              "bottomRight"
            );
            // return null;
          });
      }
    },
    saveDocuments() {
      if (!this.data.title) {
        this.openNotificationWithIcon(
          "error",
          "Please enter Document title.",
          "bottomRight"
        );
        return;
      }
      if (!this.data.url) {
        this.openNotificationWithIcon(
          "error",
          "Please upload Document.",
          "bottomRight"
        );
        return;
      }
      axios
        .post(this.APIServer + "admin/document/save", this.data, {
          headers: { Authorization: this.$store.state.token },
        })
        .then((response) => {
          this.openNotificationWithIcon(
            "success",
            response.data.data,
            "bottomRight"
          );
          this.data = {
            url: null,
            title: null,
          };
        })
        .catch((e) => {
          this.openNotificationWithIcon(
            "error",
            "Internal server error",
            "bottomRight"
          );
        });
    },

    openNotificationWithIcon(type, message, place) {
      this.$notification[type]({
        message: "Response",
        description: message,
        place,
      });
    },
  },
  // components: {
  //   TheHeaderDropdownAccnt
  // }
};
</script>