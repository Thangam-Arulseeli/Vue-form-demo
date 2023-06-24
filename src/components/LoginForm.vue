<template>
    <!-- <form>  -->
<div class="container">
  <label> EMail: </label>  
  <!-- <input type="text" placeholder="Email" 
        v-model="email" required/>
     -->
<input type="text" placeholder="Email" 
        v-model="state.email" required/>
  <span v-if="vc$.email.$error"> {{ vc$.email.$errors[0].$message }}</span>   

    </div>
<div>
    <label> Password: </label>  
    <!-- <input type="password" placeholder="Password"
       v-model="password.password" /> -->
    
       <input type="password" placeholder="Password"
       v-model="state.password.password" />
       <span v-if="vc$.password.password.$error"> {{ vc$.password.password.$errors[0].$message }}</span>   
    </div>
<div>
    <label> Confirm Password: </label>  
    <!-- <input type="password" placeholder="Confirm Password" 
        v-model="password.confirm" /> -->
        <input type="password" placeholder="Confirm Password" 
        v-model="state.password.confirm" />
        <span v-if="vc$.password.confirm.$error"> {{ vc$.password.confirm.$errors[0].$message }}</span>   
    </div>
<div>
    <button @click="submitForm">Submit</button>
</div>

<!-- </form> -->
</template>

<script>

import { useVuelidate } from '@vuelidate/core'
import { helpers } from '@vuelidate/validators';
import { required,email,minLength,maxLength, sameAs } from '@vuelidate/validators'

import {reactive, computed} from 'vue';

export default{
    setup(){
        const state = reactive({
          email: '', 
          password: {
            password: '',
            confirm: '',
          } ,
        })

        // Custom validations
        const customValidations = (value) => !value.includes('illlegal')

        const rules = computed(() => {
            return{
            email: { 
                required, 
                email,
                customValidations: helpers.withMessage('Custom Validation - eMailId shouldn\'t include restricted word',customValidations)
             },
            password: {
                password: { required, minLength: minLength(6), maxLength: maxLength(10)},
                confirm: { required, sameAs: sameAs(state.password.password)}
            },
        }
        })

        const vc$ = useVuelidate(rules, state)

        return{ state, vc$}
    },
 methods: {
    submitForm(){
        this.vc$.$validate();
            if (!this.vc$.$error){
            alert("Form submitted successfully")
        } 
        else {
            alert('Form validations failed');
        }   
    }
 }
}
</script>


<!-- export default{
    data(){
        return{
            v$: useVuelidate(),
            email: '',
            password: {
                password: '',
                confirm: ''
            }
        }
    },
    validations(){
        return{
            email: { required},
            password: {
                password: { required},
                confirm: { required}
            }
        }
    },
    methods: {
        submitForm(){
            this.v$.$validate();
            if (!this.v$.$error){
            alert("Form submitted successfully")
        } 
        else {
            alert('Form validations failed');
        }
    }
    }
}
</script> -->

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
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
</style>