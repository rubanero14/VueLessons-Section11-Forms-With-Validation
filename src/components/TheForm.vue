<template>
  <form @submit.prevent="submitForm">
    <div class="form-control-2" :class="{invalid: userNameValidity === 'invalid', valid: userNameValidity === 'valid'}">
      <label for="user-name">Your Name</label>
      <input id="user-name" name="user-name" type="text" v-model.trim="userName" @blur="validateUserName"/>
      <p v-if="userNameValidity === 'invalid'">Please enter a valid name!</p>
      <p v-if="userNameValidity === 'valid'">Awesome!</p>
    </div>
    <div class="form-control-2" :class="{invalid: userAgeValidity === 'invalid', valid: userAgeValidity === 'valid'}">
      <label for="age">Your Age (Years)</label>
      <input id="age" name="age" type="number" v-model.trim="userAge" ref="ageInput" @blur="validateUserAge"/>
      <p v-if="userAgeValidity === 'invalid'">Please enter a valid age!</p>
      <p v-if="userAgeValidity === 'valid'">Awesome!</p>
    </div>
    <div class="form-control-2">
      <label for="referrer">How did you hear about us?</label>
      <select id="referrer" name="referrer" v-model="referrer">
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <div class="form-control-2" :class="{invalid: checkboxValidity === 'invalid'}">
      <h2>What are you interested in?</h2>
      <div>
        <input id="interest-news" name="interest" type="checkbox" value="news" v-model="interest" @blur="validateCheckbox"/>
        <label for="interest-news">News</label>
      </div>
      <div>
        <input id="interest-tutorials" name="interest" type="checkbox" value="tutorials" v-model="interest" @blur="validateCheckbox"/>
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input id="interest-nothing" name="interest" type="checkbox" value="nothing" v-model="interest" @blur="validateCheckbox"/>
        <label for="interest-nothing">Nothing</label>
      </div>
      <p v-if="checkboxValidity === 'invalid'">Choose any of the options here!</p>
    </div>
    <div class="form-control-2" :class="{invalid: radioValidity === 'invalid'}">
      <h2>How do you learn?</h2>
      <div>
        <input id="how-video" name="how" type="radio" value="video-courses" v-model="how" @blur="validateRadio"/>
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input id="how-blogs" name="how" type="radio" value="blogs" v-model="how" @blur="validateRadio"/>
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input id="how-other" name="how" type="radio" value="other" v-model="how" @blur="validateRadio"/>
        <label for="how-other">Other</label>
      </div>
      <p v-if="radioValidity === 'invalid'">Choose any of the options here!</p>
    </div>
    <div class="form-control-2">
      <rating-control v-model="rating"></rating-control>
    </div>
    <div class="form-control-2" :class="{invalid: confirmTermsValidity === 'invalid'}">
        <input type="checkbox" id="confirm-terms" name="confirm-terms" v-model="confirmTerms" @blur="validateTerms"/>
        <label for="confirm-terms">Accept Terms?</label>
        <p v-if="confirmTermsValidity === 'invalid'">Please accept terms to proceed!</p>
    </div>
    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>

<script>
import RatingControl from './RatingControl.vue';

export default {
  components: {
    RatingControl,
  },
  data(){
    return {
      userName: '',
      userAge: null,
      referrer: 'wom',
      interest: [],
      how: null,
      confirmTerms: false,
      userNameValidity: 'pending',
      userAgeValidity: 'pending',
      checkboxValidity: 'pending',
      radioValidity: 'pending',
      confirmTermsValidity: 'pending',
      rating: null,
    };
  },
  methods: {
    submitForm(){
      console.log('Username: '+ this.userName);
      this.userName = '';
      console.log('Age: ');
      console.log(this.userAge);
      // console.log(typeof 36);
      // console.log(typeof this.$refs.ageInput.value);
      this.userAge = null;
      console.log('Referrer: '+this.referrer);
      this.referrer = 'wom';
      console.log('Checkboxes:');
      console.log(this.interest);
      console.log('Radio Buttons:');
      console.log(this.how);
      this.interest = [];
      this.how = null;
      console.log('Confirm Terms?');
      console.log(this.confirmTerms)
      this.confirmTerms = false;
      console.log('Rating:');
      console.log(this.rating);
      this.rating = null;
    },
    validateUserName(){
      if(this.userName === ''){
        this.userNameValidity = 'invalid';
      } else {
        this.userNameValidity = 'valid';
      }
    },
    validateUserAge(){
      if(this.userAge === null || this.userAge === ''){
        this.userAgeValidity = 'invalid';
      } else {
        this.userAgeValidity = 'valid';
      }
    },
    validateCheckbox(){
      if(this.interest.length === 0){
        this.checkboxValidity = 'invalid';
      } else {
        this.checkboxValidity = 'valid';
      }
    },
    validateRadio(){
      if(this.how === null){
        this.radioValidity = 'invalid';
      } else {
        this.radioValidity = 'valid';
      }
    },
    validateTerms(){
      if(this.confirmTerms === false){
        this.confirmTermsValidity = 'invalid';
      } else {
        this.confirmTermsValidity = 'valid';
      }
    },
  },
}
</script>


<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control-2 {
  margin: 0.5rem 0;
}

.form-control-2.invalid input {
  border-color: red;
}

.form-control-2.invalid label, .form-control-2.invalid p {
  color: red;
}

.form-control-2.valid input {
  border-color: green;
}

.form-control-2.valid label, .form-control-2.valid p {
  color: green;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>