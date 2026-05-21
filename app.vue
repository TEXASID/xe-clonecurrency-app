<template>
  <div id="app">
    <h1>Job Application Dashboard</h1>

    
    <div class="tabs">
      <button :class="{ active: currentTab === 'form' }" @click="currentTab = 'form'">
        Applicant Form
      </button>

      <button :class="{ active: currentTab === 'dashboard' }" @click="currentTab = 'dashboard'">
        Administrator Dashboard
      </button>
    </div>

  
    <div v-if="currentTab === 'form'" class="form-container">
      <h2>Applicant Form</h2>

      <form @submit.prevent="submitApplication">

        <label>Firstname</label>
        <input type="text" v-model="applicant.firstname" required />

        <label>Surname</label>
        <input type="text" v-model="applicant.surname" required />

        <label>Date of Birth</label>
        <input type="date" v-model="applicant.dob" required />

        <label>Address</label>
        <textarea v-model="applicant.address" rows="4" required></textarea>

        <label>Phone Number</label>
        <input type="tel" v-model="applicant.phone" required />

        <label>Gender</label>

        <div class="radio-group">
          <label>
            <input type="radio" value="Male" v-model="applicant.gender" />
            Male
          </label>

          <label>
            <input type="radio" value="Female" v-model="applicant.gender" />
            Female
          </label>

          <label>
            <input type="radio" value="Other" v-model="applicant.gender" />
            Other
          </label>
        </div>

        <label>National ID</label>
        <input type="text" v-model="applicant.nationalId" required />

        <button type="submit" class="submit-btn">
          Submit Application
        </button>
      </form>

      <p v-if="successMessage" class="success">
        {{ successMessage }}
      </p>
    </div>

    
    <div v-if="currentTab === 'dashboard'" class="dashboard">
      <h2>Administrator Dashboard</h2>

      <p v-if="applications.length === 0">
        No applicants yet
      </p>

      <table v-else>
        <thead>
          <tr>
            <th>Firstname</th>
            <th>Surname</th>
            <th>DOB</th>
            <th>Address</th>
            <th>Phone</th>
            <th>Gender</th>
            <th>National ID</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(app, index) in applications" :key="index">
            <td>{{ app.firstname }}</td>
            <td>{{ app.surname }}</td>
            <td>{{ app.dob }}</td>
            <td>{{ app.address }}</td>
            <td>{{ app.phone }}</td>
            <td>{{ app.gender }}</td>
            <td>{{ app.nationalId }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
  import "./style.css";

  export default {
    name: "App",

    data() {
      return {
        currentTab: "form",

        successMessage: "",

        applications: [],

        applicant: {
          firstname: "",
          surname: "",
          dob: "",
          address: "",
          phone: "",
          gender: "",
          nationalId: ""
        }
      };
    },

    methods: {
      submitApplication() {

        this.applications.push({ ...this.applicant });

        this.successMessage =
          "Application submitted successfully!";

        this.applicant = {
          firstname: "",
          surname: "",
          dob: "",
          address: "",
          phone: "",
          gender: "",
          nationalId: ""
        };

        setTimeout(() => {
          this.successMessage = "";
        }, 3000);
      }
    }
  };
</script>