<template>
    <form> 
<!-- <div class="container"> -->
  <label> EMail: </label>  
  <input type="text" placeholder="Email" 
        v-model="email" required/>
<!-- </div> -->
<!-- <div class="container"> -->
    <label> Password: </label>
    <input type="password" placeholder="Password"
       v-model="password" />
<!-- </div> -->

<!-- <div class="container"> -->
    <label> Role: </label>
    <select v-model="role">
        <option value="developer"> Web Developer</option>
        <option value="designer"> Web Designer</option>
    </select>
<!-- </div> -->

<label></label>
<div class="terms">
<input type="checkbox" v-model="terms" required>
<label> Accept Terms and Conditions </label>
</div>

<div>
    <input type="checkbox" v-model="names" value="CGVAK">
    <label>CGVAK</label>
</div>
<div>
    <input type="checkbox" v-model="names" value="G2">
    <label>G2</label>
</div>
<div>
    <input type="checkbox" v-model="names" value="CG-BLR">
    <label>CG-BLR</label>
</div>
<!--
    <div>
    <button @click="submitForm">Submit</button>
</div>
-->
</form>
<p> Email: {{ email }} </p>
<p> Password: {{ password }}</p>
<p> Role Selected: {{ role }}</p>
<p> Terms accepted: {{ terms }} </p>
<p> Names: {{ names }}</p>
</template>

<script>
// import usevalidate from '@validate/core'
// import { required } from '@validate/validators'

 export default{
//     data(){
//         return{
//             v$: usevalidate(),
//             email: '',
//             password: {
//                 password: '',
//                 confirm: ''
//             }
//         }
//     },
//     validations(){
//         return{
//             email: { required},
//             password: {
//                 password: { required},
//                 confirm: { required}
//             }
//         }
//     },
//     methods: {
//         submitForm(){
//             alert("Form submitted successfully")
//         }
//     }

data(){
    return{
        email: '',
        password: '',
        role: '',
        terms: true,
        names: []
    }
}
}
</script>

<style>
form{
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
}
</style>