<template>
  <form @submit.prevent="handleSubmit">
    <label for="email">Email</label>
    <input type="email" name="email" id="email" v-model="email">
    
    <label for="password">Password</label>
    <input type="password" name="password" id="password" v-model="password">
    <div v-if="pwdErr" class="err">{{pwdErr}}</div>
    <p></p>

    <label>Role</label>
    <select name="role" id="role" v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>
    
    <!-- <div>
        <input type="checkbox" value="apple" v-model="names">
        <label>Apple</label>
    </div>
    <div>
        <input type="checkbox" value="orange" v-model="names">
        <label>Orang</label>
    </div>
    <div>
        <input type="checkbox" value="banana" v-model="names">
        <label>Banana</label>
    </div>     -->

    <label>Skills</label>
    <input type="text" v-model="tempskill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" @click="delSkill(skill)">
        {{ skill }}
    </div>
        <div class="terms">
        <input type="checkbox" v-model="terms" required id="terms">
        <label for="terms">Accept terms and conditions</label>
    </div>
    <div class="submit">
        <button type="submit">Create Account</button>
    </div>
  </form>

  <p>Email: {{email}}</p>
  <p>Pwd: {{password}}</p>
  <p>Role: {{role}}</p>
  <p>Terms: {{terms}}</p>
  <p>Names: {{names}}</p>

</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role:'designer',
            terms: false,
            names: [],
            tempskill: '',
            skills:[],
            pwdErr: ''
        }
    },
    methods: {
        addSkill(e) {
            if (e.key === ',' && this.tempskill) {
                if (!this.skills.includes(this.tempskill)) {
                    this.skills.push(this.tempskill);
                }
                this.tempskill = '';
            }
        },
        delSkill(target){
            // var tarindex = this.skills.indexOf(target);
            // this.skills.splice(tarindex, 1);

            this.skills = this.skills.filter(skill=>{
                return skill !== target
            })
        },
        handleSubmit(){
            this.pwdErr = this.password.length > 5? '': 'Password must be at least 6 characters.'
            if (!this.pwdErr) {
                console.log('form submitted');
                console.log('email: ', this.email);
                console.log('password: ', this.password);
                console.log('role: ', this.role);
                console.log('skills: ', this.skills);
            }
        }
    },
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6rem;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill{
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    .submit{
        text-align: center;
    }
    .submit button{
        background: rgb(74, 121, 250);
        border: 0;
        margin-top: 20px;
        padding: 10px 20px;
        color: white;
        border-radius: 20px;
    }
    .err{
        color: rgb(222, 0, 0);
        margin-top: 10px;
        font-size: 0.5rem;
    }
</style>