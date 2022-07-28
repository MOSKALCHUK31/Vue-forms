<template>
  <form @submit.prevent="onSubmit">
    <div class="form-control" :class="{invalid: validatedName === 'invalid'}">
      <label for="user-name">Your Name</label>
      <input id="user-name" name="user-name" type="text" v-model.trim="name" @blur="validateInput"/>
      <p v-if="validatedName === 'invalid'">Invalid name!</p>
    </div>
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input id="age" name="age" type="number" v-model="age" ref="userAge_refs"/>
    </div>
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select id="referrer" name="referrer" v-model="referrer">
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <div class="form-control">
      <!-- For checkbox we have to bind data to array, then every checkbox must to have a idnitified value [using value attribute] -->
      <h2>What are you interested in?</h2>
      <div>
        <input id="interest-news" name="interest" type="checkbox" value="news" v-model="checkboxes"/>
        <label for="interest-news">News</label>
      </div>
      <div>
        <input id="interest-tutorials" name="interest" type="checkbox" value="tutorials" v-model="checkboxes"/>
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input id="interest-nothing" name="interest" type="checkbox" value="nothing" v-model="checkboxes"/>
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <!-- <rating-control :modelValue="rating" @update:ModelValue="show"></rating-control> -->
      <rating-control :modelValue="rating" @updateModelValue="setRating"></rating-control>
    </div>
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input id="how-video" name="how" type="radio" value="video" v-model="radio"/>
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input id="how-blogs" name="how" type="radio" value="blogs" v-model="radio"/>
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input id="how-other" name="how" type="radio" value="other" v-model="radio"/>
        <label for="how-other">Other</label>
      </div>
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
    RatingControl
  },
  data() {
    return {
      name: '',
      age: null, //null because expected type number,
      referrer: 'google', // set default value (get string from value in option)
      checkboxes: [], // If we have more than 1 checkbox, we should use array. If checkbox=checked, we will get checked values in array
      radio: null, // null because expect string if one of theese radio will be checked
      validatedName: 'pending', // default status if the input is empty
      rating: null
    }
  },
  methods: {
    onSubmit() {
      console.log(`Name: ${this.name}`);
      this.name = '';
      console.log('Age: ' + this.age); // From v-model we got type number
      this.age = null
      console.log(`Age with refs: ${this.$refs.userAge_refs.value}`); // From refs we got type string [be patient]
      console.log('Referrer: ' + this.referrer); // Got value from option (Not the same as text)
      this.referrer = 'google';
      console.log('Checkboxes: ' + this.checkboxes); // We got array values like [val1, val2, val3] if checkbox checked
      this.checkboxes = [];
      console.log('Radio: ' + this.radio); // We got value attribute from radiobutton input like 'video'
      this.radio = null;
      console.log('Rating: ' + this.rating);
      this.rating = null;
    },
    validateInput() {
      if (this.name == '') {
        this.validatedName = 'invalid'
      } else {
        this.validatedName = 'valid'
      }
    },
    setRating (option) {
      this.rating = option;
    }
  }
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

.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label,
.form-control.invalid p {
  color: red;
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