<template>
  <form @submit.prevent="handleSubmit">
    <label>Email</label>
    <input type="email" required v-model="email" placeholder="Enter your email" />
    <label>password</label>
    <input
      type="password"
      required
      v-model="password"
      placeholder="Enter your password"
    />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role: </label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills: </label>
    <input type="skill" v-model="tempSkill" @keyup="addSkill" />

    <div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill">
      {{ skill }}
    </div>

    <div>
      <input type="checkbox" value="promotions" v-model="names" />
      <label>Promotions</label>
    </div>
    <div>
      <input type="checkbox" value="newsletter" v-model="names" />
      <label>Newsletter</label>
    </div>
    <div>
      <input type="checkbox" value="subscribe" v-model="names" />
      <label>subscribe</label>
    </div>
    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>I agree to the terms and conditions</label>
    </div>
    <div><button type="submit">Sign Up</button></div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms accepted: {{ terms }}</p>
  <p>Names: {{ names }}</p>
</template>

<script>
export default {
  name: "SignupForm",
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      names: [],
      skills: [],
      passwordError: "",
    };
  },
  props: {},
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (this.skills.includes(this.tempSkill)) {
          alert("Skill already exists");
        } else {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills.splice(this.skills.indexOf(skill), 1);
      // this.skills = this.skills.filter((item) =>{
      //   return item !== skill
      // })
    },
    handleSubmit(e) {
      // e.preventDefault()

      // validate password
      this.passwordError =
        this.password.length > 5 ? "" : "Password must be at least 6 characters";

      if (this.passwordError) {
        console.log("email: ", this.email);
        console.log("password: ", this.password);
        console.log("role: ", this.role);
        console.log("terms: ", this.terms);
        console.log("skills: ", this.skills);
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input:focus,
select:focus {
  outline: none;
  border-bottom: 1px solid #aaa;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.terms {
  margin: 20px 0;
}
button {
  display: block;
  width: 100%;
  padding: 10px 6px;
  border: none;
  background: #333;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  margin: 20px 0;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  cursor: pointer;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #333;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
