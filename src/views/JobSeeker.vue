<template>
    <div>
        <base-header type="gradient-success" class="pb-6 pb-8 pt-5 pt-md-8">
              <form>
              <div class="row">
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="Name">Name</label>
                    <input
                      type="text"
                      class="form-control"
                      required
                      minlength="1"
                      v-model="addJobSeekerForm.name"
                      maxlength="20"
                      id="Name"
                    />
                  </div>
                </div>
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="profile">Profile</label>
                    <input
                      type="text"
                      class="form-control"
                      required
                      minlength="1"
                      v-model="addJobSeekerForm.profile"
                      maxlength="20"
                      id="profile"
                    />
                  </div>
                </div>
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="Mobile">Mobile</label>
                    <input
                      type="text"
                      class="form-control"
                      required
                      v-model="addJobSeekerForm.mobile"
                      oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"
                      minlength="10"
                      maxlength="12"
                      id="Mobile"
                    />
                  </div>
                </div>
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="Email">Email</label>
                    <input
                      type="email"
                      v-model="addJobSeekerForm.email"
                      class="form-control"
                      required
                      id="Email"
                    />
                  </div>
                </div>
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="experience">Experience</label>
                    <input
                      type="text"
                      class="form-control"
                      required
                      minlength="1"
                      v-model="addJobSeekerForm.experience"
                      maxlength="10"
                      oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"
                      id="experience"
                    />
                  </div>
                </div>
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="duration">Duration</label>
                    <input
                      type="text"
                      class="form-control"
                      required
                      v-model="addJobSeekerForm.duration"
                      minlength="1"
                      maxlength="10"
                      oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"
                      id="duration"
                    />
                  </div>
                </div>
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="isQuizRequired">IsQuizRequired</label>
                    <select class="form-control" v-model="selected">
                      <option selected value="">Select Option</option>
                      <option value="true">Yes</option>
                      <option value="false">No</option>
                    </select>
                  </div>
                </div>
                <div class="col-sm-3">
                  <div class="form-group">
                    <label for="address">Address</label>
                    <textarea
                      type="text"
                      v-model="addJobSeekerForm.address"
                      class="form-control"
                      rows="1"
                      id="address"
                    />
                  </div>
                </div>
              </div>
              <div class="row">
                <div class="col-sm-5"></div>
                <div class="col-sm-2">
                  <button type="submit" class="btn btn-dark btn-lg btn-block">
                    Save
                  </button>
                </div>
                <div class="col-sm-5"></div>
              </div>   </form>
        </base-header>
         <link
            href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"
            rel="stylesheet"
            integrity="sha384-wvfXpqpZZVQGK6TAh5PVlGOfQNHSoD2xbE+QkPxCAFlNEevoEH3Sl0sibVcOQVnN"
            crossorigin="anonymous"
          />
        <div class="container-fluid mt--7">
            <div class="row">
                <div class="col">
                    <div class="card shadow">
                        <div class="card-header bg-transparent">
                            <h3 class="mb-0"> View Job Seeker</h3>
                        </div>
                        <div class="card-body">
                            <div class="row">
                            <div class="container">
          <div class="row">
            <div class="col-sm-12">
              <main>
                <data-table
                  v-bind="parameters"
                  @actionTriggered="handleAction"
                />
              </main>
            </div>  </div>
          </div>
                                <!-- <div class="col-lg-3 col-md-6"
                                     v-for="(icon, index) in JobSeeker" :key="icon.name + index">
                                    <button type="button"
                                            v-b-tooltip.hover.top
                                            :title="icon.name"
                                            v-clipboard:copy="icon.name"
                                            v-clipboard:success="onCopy"
                                            class="btn-icon-clipboard" data-clipboard-text="air-baloon">
                                        <div>
                                            <i :class="icon.name"></i>
                                            <span>{{icon.name.substring(6)}}</span>
                                        </div>
                                    </button>
                                </div> -->
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
<script>
  import io from "../../config";
  import axios from "axios";
  import Vue from 'vue'
  import VueClipboard from 'vue-clipboard2'
  import BTooltipDirective from 'bootstrap-vue/esm/directives/tooltip'
  
  Vue.use(VueClipboard)
  export default {
    directives: {
      'b-tooltip': BTooltipDirective
    }, computed: {
    parameters() {
      return {
        data: this.dataTableData,
        actionMode: "single",
        columns: [
          {
            key: "name",
            title: "Name",
          },
          {
            key: "email",
            title: "Email",
          },
          {
            key: "contact",
            title: "Contact",
          },
          {
            key: "profile",
            title: "Profile",
          },
            {
            key: "experience",
            title: "Experience",
          },
            {
            key: "duration",
            title: "Duration",
          },
            {
            key: "isQuizRequired",
            title: "Quiz Required",
          },
           {
            key: "quizMailReceived",
            title: "QuizMailReceived",
          },
           {
            key: "testGiven",
            title: "testGiven",
          },
           {
            key: "resultMailReceived",
            title: "resultMailReceived",
          },
           {
            key: "status",
            title: "status",
          },
        ],
      };
    },
  },
    data() {
    return {
      dataTableData: [],
      error: [],
      selected: "",
      addJobSeekerForm: {
        name: null,
        profile: null,
        email: null,
        mobile: null,
        experience: null,
        duration: null,
        isQuizRequired: null,
        address: null,
      },
    };
    },
    methods: {
     handleAction(action, payload) {
      console.log(action, payload);
      window.alert("check out the console to see the data logged");
    }
    },
      mounted() {
    axios({
      method: "get",
      url: `${io.baseURL}/common/getJobSeekerInfo`,
    })
      .then(
        (response) => (
          console.log("----------", response.data.data),
          (this.dataTableData = response.data.data)
        )
      )
      .catch((error) => {
        console.log(error);
      });
  },
  };
</script>
<style></style>
