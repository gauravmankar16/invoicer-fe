<template>
  <section class="section has-background-light same-page-height" >
    <div class="columns">
      <div class="column is-4 is-offset-4  box">
        <h1 class="title is-1 has-text-primary has-text-centered">Start with Invoicer!</h1>
        <p class="has-text-centered has-text-black has-text-weight-bold mt2 mb1">Personal Details</p>
        <!--   Email     -->
        <div class="columns">
          <div class="column">
            <b-field label="Email">
              <b-input
                placeholder="Email"
                type="email"
                v-model="biller.email"
              >
              </b-input>
            </b-field>
          </div>
        </div>
        <!--  Name  -->
        <div class="columns">
          <div class="column">
            <b-field label="First Name">
              <b-input
                placeholder="First Name"
                v-model="biller.name.first"
              >
              </b-input>
            </b-field>
          </div>
          <div class="column">
            <b-field label="Last Name">
              <b-input
                placeholder="Last Name"
                v-model="biller.name.last"
              >

              </b-input>
            </b-field>
          </div>
        </div>
        <!--  Address  -->
        <p class="has-text-centered has-text-black has-text-weight-bold mt2 mb1">Address</p>
        <div class="columns">
          <div class="column">
            <b-field label="Street">
              <b-input placeholder="Street"
                       v-model="biller.address.street">
              </b-input>
            </b-field>
          </div>
          <div class="column">
            <b-field label="Apartment No">
              <b-input placeholder="Apartment Number"
                       v-model="biller.address.apartmentNumber">

              </b-input>
            </b-field>
          </div>
        </div>
        <div class="columns">
          <div class="column">
            <b-field label="City">
              <b-input placeholder="City"
                       v-model="biller.address.city"
              >
              </b-input>
            </b-field>
          </div>
          <div class="column">
            <b-field label="Postal Code">
              <b-input placeholder="Postal Code"
                       v-model="biller.address.postalCode"
              >
              </b-input>
            </b-field>
          </div>
        </div>
        <!--  Details  -->
        <p class="has-text-centered has-text-black has-text-weight-bold mt2 mb1">Other</p>
        <div class="columns">
          <div class="column">
            <b-field label="IBAN">
              <b-input placeholder="IBAN"
                       v-model="biller.iban">
              </b-input>
            </b-field>
          </div>

        </div>
        <div class="columns">
          <div class="column">
            <b-field label="Company Name">
              <b-input placeholder="Company Name"
                       v-model="biller.company"
              >
              </b-input>
            </b-field>
          </div>
        </div>
        <!--   Password   -->
        <div class="columns">
          <div class="column">
            <b-field label="Password">
              <b-input placeholder="Password"
                       v-model="biller.company"
                       type="password"
              >
              </b-input>
            </b-field>
          </div>
        </div>
        <!--  register button  -->
        <div class="columns">
          <div class="column">
            <div class="field is-grouped is-grouped-centered">
              <p class="control">
                <button class="button is-primary" @click="registerBiller">
                  Submit
                </button>
              </p>
            </div>
          </div>
        </div>

        <div class="columns">
          <div class="column has-text-centered has-text-black ">
            <a href="/#/login">Already have an account? </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  const baseUrl = process.env.VUE_APP_API_SERVER;
  import axios from 'axios';

  export default {
    name: "RegisterBiller.vue"
    , mounted() {
      this.axiosInstance = axios.create({
        baseURL: baseUrl,
        headers: {
          'Content-Type': 'application/json',
        }
      });
    },
    data(){
      return {
        biller:{
          iban:"",
          company:"",
          password:"",
          email:"",
          name:{
            first:"",
            last:""
          },
          address:{
            street:"",
            apartmentNumber:"",
            city:"",
            postalCode:"",
            country:"India"
          }
        }
      }
    },
    methods:{
      registerBiller(){
        this.axiosInstance.post('/biller',this.$data.biller)
          .then(response=>{
            console.log(response);
            this.$buefy.toast.open({
              duration: 3000,
              message: `Biller Registered`,
              position: 'is-bottom',
              type: 'is-success'
            })
            this.$router.push('/dashboard/biller-list');
          })
          .catch(error=>{
            console.error(error);
            this.$buefy.toast.open({
              duration: 3000,
              message: `Something went wrong`,
              position: 'is-bottom',
              type: 'is-danger'
            })
          })
      }
    }
  }
  undefined
</script>

<style scoped>

</style>
