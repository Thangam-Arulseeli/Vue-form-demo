<template>
<!-- https://www.youtube.com/watch?v=3qkbrIYMXOk&pp=ygUWdnVlIDMgZm9ybSB2YWxpZGF0aW9uIA%3D%3D 
https://www.youtube.com/watch?v=ptHIHN2qDts&pp=ygUWdnVlIDMgZm9ybSB2YWxpZGF0aW9uIA%3D%3D
-->

<div class="row mb-3 col-sm-5 align-center bg-success text-worning"> <h2> Account Creation Form</h2> </div>

<div class="py-3">

<form @submit.prevent="handleSubmit" class="">

<div class="row mb-3">
    <label for="name" class="col-sm-2 col-form-label"> Name </label>
    <div class="col-sm-3">
       <input type="text" class="form-control" id="name" name="name" v-model="name" required placeholder="" /> 
    </div>
</div>

<div class="row mb-3">
    <label for="email" class="col-sm-2 col-form-label"> Email </label>
    <div class="col-sm-3">
       <input type="email" class="form-control" id="email" name="email" v-model="mailid" required placeholder="example@gmail.com"/> 
    </div>
</div>

<div class="row mb-3">
    <label for="password" class="col-sm-2 col-form-label"> Password </label>
    <div class="col-sm-3">
       <input type="password" class="form-control" id="pword" name="pword" v-model="pword" required placeholder="" /> 
        <div v-if="passwordError"> {{ passwordError }} </div>
    </div>
</div>

<div class="row mb-3">
    <label for="role" class="col-sm-2 col-form-label"> Role </label>
    <div class="col-sm-3">
      <select class="form-control" id="role" name="role" v-model="role">  
        <option value="Developer"> Web Developer</option>
        <option value="Designer"> Web Designer </option>
        <option value=".Net"> .Net Developer </option>
        <option value="Tester"> System Tester </option>
       <option value="Back-End-Admin"> Data Base Administrator </option>
      </select>  
    </div>
</div>

<div class="row mb-3">
    <label for="names" class="col-sm-2 col-form-label"> Select Software </label>
    <div class="col-sm-3 align-left">
        <div>
             <input type="checkbox" value="Java" v-model="names">
            <label> Java </label>
        </div>
        <div>
             <input type="checkbox" value="PHP" v-model="names">
            <label> PHP </label>
        </div>
        <div>
             <input type="checkbox" value="Angular" v-model="names">
            <label> Angular </label>
        </div>
        <div>
            <input type="checkbox" value="Vue JS" v-model="names">
            <label> Vue JS </label>
        </div>
        <div>
            <input type="checkbox" value="React" v-model="names">
            <label> React </label>
        </div>

    </div>
</div>

<div class="row mb-3">
    <label for="skilllist" class="col-sm-2 col-form-label"> Extra Skills </label>
    <div class="col-sm-3">
        <input type="text" class="form-control"  v-model="tempskill" @keyup="addSkill">
            <div v-for="skill in skills" :key="skill">
            <span class="pill" @click="deleteSkill(skill)">  {{ skill }}  </span> </div>
    </div>
</div>

<div class="row mb-3">
    <input type="checkbox" class="col-sm-2" v-model="terms" required>
    <div class="col-sm-3">
        <label for="terms" class="col-form-label"> Accept terms and conditions </label>
    </div>
</div>

<div class="row mb-3 submit">
   <button type="submit" class="btn col-sm-5 btn-primary"> Create an Account </button>
</div>

 </form>
</div>

<div class="container text-left bg-secondary text-warning">
  <p> Name : {{name}} </p>  
  <p> Email ID : {{ mailid }}  </p>
  <p> Password : {{ pword }}  </p>
  <p> Role : {{ role }}  </p>
  <p> Software Selected : {{names}} </p>
  Extra Skills <p  v-for="skill in skills" :key="skill"> 
  <span> {{ skill }} </span> </p>
  <p> Terms accepted : {{ terms }} </p>
 </div>


</template>


<script>
export default{
    data(){
        return{
            name : 'Seeli',
            mailid: 'seeli@gmail.com',
            pword: '',
            role: '.Net',
            terms: false,
            names: [],
            tempskill: '',
            skills: [],
            passwordError: ''

        }
    },
    methods: {
        addSkill(e){
           // console.log(e);
            if (e.key === ',' && this.tempskill) {
               if(!this.skills.includes(this.tempskill)){
                    this.skills.push(this.tempskill)
                    this.tempskill=''
               }
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit(){
           console.log('Form Submitted')
           this.passwordError = this.pword.length > 5 ? '' : 'Password must be atleast 6 characters long'
           if(!this.passwordError){
               console.log('Name     : ', this.name)
               console.log('Email ID : ', this.mailid)
               console.log('Password : ', this.pword)
               console.log('Role     : ', this.role)
               console.log('Skills   : ', this.skills)
               console.log('Terms Accepted : ', this.terms)

           }
        }

    }

}
</script>

<style>
/* form{
    max-width: 420px;
    margin: 30px auto;
    background: #999;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #555;
    display:inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color : #555;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px; 
}  */
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding:  6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
</style>