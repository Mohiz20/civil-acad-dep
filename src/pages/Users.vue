<template>
  <div class="users">
    <div class="row">
      <div class="col-md-12">
        <div class="card">
          <div class="card-body">
            <div class="row">
              <div class="col-md-6 col-lg-6 col-xl-6 col-6 col-sm-6 col-xs-6">
                <h5><strong>Users</strong></h5>
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
                  <b-dropdown-item @click="csvExport()">CSV</b-dropdown-item>
                  <b-dropdown-item @click="exportPDF()">PDF</b-dropdown-item>
                </b-dropdown>
                <button class="btn btn-primary" @click="move('/create-user')">
                  <i class="fa fa-plus"></i> Create User
                </button>
              </div>
            </div>
            <div class="row my-3">
              <div class="col-12 col-md-3">
                <label for="filter"><strong>Filter By Status</strong></label>
                <select class="form-control" @change="filterUserList()" v-model="filterObject.status">
                  <option :value="null">Filter Users By Status</option>
                  <option value="all">All</option>
                  <option value=1>Active</option>
                  <option value=0>Inactive</option>
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
                  @keyup = "filterUserList()"
                  v-model = "filterObject.name_phone"
                />
              </div>
              <div class="col-12 col-md-3 mt-md-0 mt-3">
                <label for="filter"><strong>Search By Email</strong></label>
                <input
                  type="text"
                  placeholder="Search By Email"
                  class="form-control"
                  @keyup = "filterUserList()"
                  v-model = "filterObject.email"
                />
              </div>
              <div class="col-12 col-md-3 mt-md-0 mt-3">
                <label for="filter"><strong>Search By Date</strong></label>
                <a-range-picker class="date-input" size="default" @change="filterUserList()" v-model = "dateRange"/>
              </div>
            </div>
            <div class="row">
              <div class="col-md-12">
                <a-table
                  class="table"
                  :columns="columns"
                  :dataSource="userList"
                  :scroll="{ x: 2300 }"
                  :loading="loading"
                >
                  <span slot="image" slot-scope="id, record">
                    <b-img
                      v-bind="mainProps1"
                      :src="record.image"
                    ></b-img>
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
                    <i class="fa fa-trash" @click="deleteme(record)"></i>
                  </span>
                </a-table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- <b-modal v-model="editModal" hide-footer title="Edit User">
            <div class="row mb-3">
                <div class="col-12 text-center">
                    <div class="image" @click="pickAvatar" v-bind:style="{ 'background-image': 'url(' + image + ')' }">
                        <div v-if="!image">
                            <i class="fa fa-camera" ></i>
                            <p>Upload Image</p>
                        </div> 
                    </div>
                    <input type="file" class="btn btn-primary" style="display:none" accept="image/*"  @change="onAvatarSelected" ref="AvatarInput">
                </div>
            </div>
            <form @submit.prevent="update">
                <div class="row" v-if="editUser">
                    <div class="col-6 mt-2">
                        <div class="form-group">
                            <label for="first_name"><strong>First Name*</strong></label>
                            <input type="text" class="form-control" v-model="editUser.first_name" placeholder="Enter First Name" required>
                        </div>
                    </div>
                    <div class="col-6 mt-2">
                        <div class="form-group">
                            <label for="last_name"><strong>Last Name*</strong></label>
                            <input type="text" class="form-control" v-model="editUser.last_name" placeholder="Enter Last Name" required>
                        </div>
                    </div>
                    <div class="col-6 mt-2">
                        <div class="form-group">
                            <label for="email"><strong>Email*</strong></label>
                            <input type="email" class="form-control" v-model="editUser.email" placeholder="Enter Email" required>
                        </div>
                    </div>
                    <div class="col-6 mt-2">
                        <div class="form-group">
                            <label for="mobile"><strong>Mobile*</strong></label>
                            <input type="tel" class="form-control" v-model="editUser.mobile" placeholder="Enter Mobile" required>
                        </div>
                    </div>
                    <div class="col-6 mt-2">
                        <div class="form-group">
                            <label for="job_title"><strong>Job Title*</strong></label>
                            <input type="text" class="form-control" v-model="editUser.job_title" placeholder="Enter Job Title" required>
                        </div>
                    </div>
                    <div class="col-6 mt-2">
                        <div class="form-group">
                            <label for="nationality"><strong>Nationality*</strong></label>
                            <input type="text" class="form-control" v-model="editUser.nationality" placeholder="Enter Nationality" required>
                        </div>
                    </div>
                    <div class="col-12 mt-3">
                        <button class="btn btn-primary btn-block">Edit User</button>
                    </div>
                </div>
            </form>
            
        </b-modal> -->

    <b-modal v-model="viewModal" hide-footer title="User Details">
      <div class="row">
      <div class="col-12 text-center mt-2 mb-3">
          <img v-bind="mainProps1" :src="viewUser.image" height="150" width="150"></img>
        </div>
        <div class="col-12 text-center mt-2 mb-3">
          <p>
            <strong class="text-main"
              >Last Edited By Admin {{ viewUser.updated_at }}</strong>
          </p>
        </div>
        <!-- <div class="col-12 text-center mt-2 mb-3">
                    <b-img v-bind="mainProps" src="https://ptetutorials.com/images/user-profile.png"></b-img>
                </div> -->
        <div class="col-12 col-md-6 mt-2">
          <label for="id"><strong>User Id</strong></label>
          <p>{{ viewUser.id }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="id"><strong>Registration Date</strong></label>
          <p>{{ viewUser.created_at }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="first_name"><strong>First Name</strong></label>
          <p>{{ viewUser.first_name }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="last_name"><strong>Last Name</strong></label>
          <p>{{ viewUser.last_name }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="email"><strong>Email</strong></label>
          <p>{{ viewUser.email }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="mobile"><strong>Mobile</strong></label>
          <p>{{ viewUser.phone }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="status"><strong>Status</strong></label>
          <p>{{ viewUser.status?'Active' : 'Inactive' }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="gender"><strong>Gender</strong></label>
          <p>{{ viewUser.gender }}</p>
        </div>
        <!-- <div class="col-12 col-md-6 mt-2">
          <label for="job"><strong>Job Title</strong></label>
          <p>Software Engineer</p>
        </div> -->
        <div class="col-12 col-md-6 mt-2">
          <label for="nationality"><strong>Country</strong></label>
          <p>{{ viewUser.country }}</p>
        </div>
        <div class="col-12 col-md-6 mt-2">
          <label for="nationality"><strong>Residence</strong></label>
          <p>{{ viewUser.residence }}</p>
        </div>
      </div>
    </b-modal>
    <b-modal title="Delete Confirmation" modal-class="myclass" :hide-footer="true" v-model="deleteModal">
      <form @submit.prevent>
        <div class="row">
          <div class="col-12 mt-3">
            <div class="form-group">
              <h5 class="d-block text-center"><strong>Are you sure you want to delete it?</strong></h5> <br />
            </div>
          </div>
          <div class="col-12 mt-10 fr">
           <span>
            <button class="btn btn-secondary mr-4" @click="deleteModal=false;">Cancel</button>
            <button class="btn btn-primary" @click="deleteItem(storeRecord);">Delete</button>
            </span>
          </div>
        </div>
      </form>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";
import jsPDF from 'jspdf';
import moment from 'moment'
import countries from '../assets/countries.json'
import 'jspdf-autotable';
export default {
  name: "users",
  computed: {
    rows() {
      return this.items.length;
    },
  },
  data() {
    return {
      dateRange: null,
      deleteModal:false,
      storeRecord:{
        id: null
      },
      filterObject : {
        email : '',
        name_phone: '',
        status: null,
        date_from: '',
        date_to: ''
      },
      APIServer:  `http://cryptic-gorge-79265.herokuapp.com/api/` || process.env.VUE_APP_SERVER_ADDRESS ,
      mainProps: { blank: false, blankColor: "#777", width: 80, height: 80 },
      mainProps1: { blank: false, blankColor: "#777", width: 45, height: 45 },
      editUser: null,
      image: null,
      editModal: false,
      viewModal: false,
      //   viewUser:null,
      pagination: {},
      loading: false,
      visible: false,
      viewUser: {
        first_name: null,
        last_name: null,
        email: null,
        phone: null,
        nationality: null,
        image: null,
        job_title: null,
        status: "active",
        updated_at: null,
      },
      userList: [{
        image : null,
        id : 1,
        created_at: '01-01-2021',
        first_name: 'test',
        last_name: 'last',
        email: 'test@test.com',
        phone: 9090909090,
        country: 'India',
        residence: 'indai'
      }],
      columns: [
        {
          title: "Image",
          dataIndex: "imagePath",
          width: "6%",
          scopedSlots: { customRender: "imagePath" },
        },
        {
          title: "Id",
          dataIndex: "_id",
          width: "6%",
          sorter: (a, b, sortOrder) => a.id - b.id,
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Registration Date",
          dataIndex: "registrationTime",
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
          title: "First Name",
          dataIndex: "firstName",
          sorter: (a, b, sortOrder) => a.first_name.localeCompare(b.first_name),
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Last Name",
          dataIndex: "lastName",
          sorter: (a, b) => a.last_name.localeCompare(b.last_name),
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Email",
          dataIndex: "email",
          sorter: (a, b) => a.email.localeCompare(b.email),
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Phone",
          dataIndex: "phoneNo",
          sorter: (a, b) => a.phone.localeCompare(b.phone),
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Country",
          dataIndex: "nationality",
          sorter: (a, b) => a.country.localeCompare(b.country),
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Residence",
          dataIndex: "residenceCountry",
          dataIndex: "residenceCountry",
           sorter: (a, b) => {
            if(!a.residence){
              a.residence = '';
            }
            if(!b.residence){
              b.residence = '';
            }
            return  a.residence.localeCompare(b.residence);
          },
          sortDirections: ["descend", "ascend"],
        },
        {
          title: "Status",
          dataIndex: "status",
          scopedSlots: { customRender: "status" },
        },
        {
          title: "Actions",
          scopedSlots: { customRender: "actions" },
        },
      ],
    };
  },
  created() {
    this.getUsersList();
  },
  methods: {
    deleteme(record){
      console.log(record)
    },
    getBoolVal(val){
      if(val===1){
        return true;
      }
      else{
        return false;
      }
    },

    csvExport() {
      let arrData = [];
      arrData.push(...this.userList);
      arrData.forEach((item) => {
        delete item.image;
        delete item.id;
        delete item.nationality;
        delete item.created_at;
        delete item.updated_at;
        delete item.dob;
        delete item.email_verified_at;
      });

      let csvContent = "data:text/csv;charset=utf-8,";
      csvContent += [
        Object.keys(arrData[0]).join(";"),
        ...arrData.map(item => Object.values(item).join(";"))
      ]
      .join("\n")
      .replace(/(^\[)|(\]$)/gm, "");

      const data = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", data);
      link.setAttribute("download", "Users.csv");
      link.click();
    },

    exportPDF() {
      var vm = this;
      let columns = [];
      columns.push(...this.columns);
      columns.forEach((item) => {
        item.dataKey = item.dataIndex;
      });
      columns.shift();
      columns.pop();
      var doc = new jsPDF('p', 'pt');
      doc.text('Users List', 40, 50);
      doc.autoTable({
        margin: { top: 70 },
        headStyles: {cellPadding: 9, fillColor: [236, 142, 43] },
        bodyStyles: {cellPadding: 6 },
        body: vm.userList,
        columns: columns,
      })
      doc.save('Users.pdf');
    },
    openNotificationWithIcon(type, message) {
      this.$notification[type]({
        message: "Response",
        description: message,
      });
    },
    filterUserList() {
      if(this.dateRange && this.dateRange.length!==0 ){
          this.filterObject.date_from = moment(JSON.parse(JSON.stringify(this.dateRange[0]))).format('yyyy-MM-DD');
          this.filterObject.date_to = moment(JSON.parse(JSON.stringify(this.dateRange[1]))).format('yyyy-MM-DD');
      }
      else{
        this.filterObject.date_from = null;
        this.filterObject.date_to = null;
      }
      axios
        .post(this.APIServer + "admin/user/filter", this.filterObject, {
          headers: { Authorization: this.$store.state.token },
        })
        .then((response) => {
          if (response.data.status == "success") {
            console.log(response.data.data);
            this.userList = response.data.data;
            this.userList.forEach((item) => {
              let countryVal = countries.filter(val=>val.name===item.country);
              item.phone = countryVal[0].dial_code+" "+item.phone;
              item.created_at = item.created_at.replace('T',' ').substring(0, 19);
            });
            this.userList.reverse();
          }
          this.loading = false;
        })
        .catch((e) => {
          console.log("API failed");
          console.log(e);
          this.loading = false;
          this.openNotificationWithIcon("error", "Internal server error");
        });
    },
    getUsersList() {
      this.loading = true;
      if(this.dateRange && this.dateRange.length!==0 ){
          this.filterObject.date_from = moment(JSON.parse(JSON.stringify(this.dateRange[0]))).format('yyyy-MM-DD');
          this.filterObject.date_to = moment(JSON.parse(JSON.stringify(this.dateRange[1]))).format('yyyy-MM-DD');
      }
      else{
        this.filterObject.date_from = null;
        this.filterObject.date_to = null;
      }
      axios
        .get(this.APIServer + "admin/getUsers/", {
          headers: { Authorization: this.$store.state.token },
        })
        .then((response) => {
          console.log('response:', response)
          this.userList = response.data;
            this.userList.forEach((item) => {
              let countryVal = countries.filter(val=>val.name===item.country);
              item.phone = countryVal[0].dial_code+" "+item.phone;
              item.created_at = item.created_at.replace('T',' ').substring(0, 19);
            });
            this.userList.reverse();
          if (response.data.status == "success") {
            console.log(response.data.data);
            this.userList = response.data.data;
            this.userList.forEach((item) => {
              let countryVal = countries.filter(val=>val.name===item.country);
              item.phone = countryVal[0].dial_code+" "+item.phone;
              item.created_at = item.created_at.replace('T',' ').substring(0, 19);
            });
            this.userList.reverse();
          }
          this.loading = false;
        })
        .catch((e) => {
          console.log("API failed");
          console.log(e);
          this.loading = false;
          this.openNotificationWithIcon("error", "Internal server error");
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
      console.log(record, 'record')
      this.deleteModal=false;
      axios
        .get(this.APIServer + "admin/deleteUser/" + record.id, {
          headers: { Authorization: this.$store.state.token },
        })
        .then((response) => {
          if (response.data.status == "success") {
            this.openNotificationWithIcon(
              "success",
              "User deleted successfully"
            );
            this.filterUserList();
          }
        })
        .catch((e) => {
          console.log("API failed");
          this.openNotificationWithIcon("error", "User deleting failed");
          console.log(e);
        });
    },
    viewUserData(record) {
     
      this.viewUser = record;
      this.viewModal = !this.viewModal;
    
    },
    onChangeStatus(record) {
      axios
        .get(this.APIServer + "admin/user/toggle-status/" + record.id, {
          headers: { Authorization: this.$store.state.token },
        })
        .then((response) => {
          if (response.data.status == "success") {
            this.openNotificationWithIcon(
              "success",
              "User status toggled successfully"
            );
            this.filterUserList();
          }
        })
        .catch((e) => {
          console.log("API failed");
          this.openNotificationWithIcon("warning", "User status toggle failed");
          console.log(e);
        });
    },
  },
};
</script>