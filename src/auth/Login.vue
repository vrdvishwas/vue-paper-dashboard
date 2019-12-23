<template>
<div class="wrapper">
    <div class="row">
        <div class="col-md-4"></div>
        <div class="col-md-4 mt-5">
            
<div class="card-group">
            <div class="card p-4 bg-light">
                <div class="card-body "> 
                    
                    <form method="POST" action="" v-on:submit.prevent="submitLogin">
                        <h1 class="text-center">Login</h1>
                        <h5 class="text-danger" v-if="loginerror">Invalid login details</h5>
                        <validation-provider rules="required" v-slot="{ errors }">
                        <div class="input-group mt-3">
                            <div class="input-group-prepend">
                                <span class="input-group-text">
                                    <i class="fa fa-user"></i>
                                </span>
                            </div>
                            
                            <input name="username" type="text"
                                   class="form-control"
                                   required autofocus
                                   placeholder="Username"
                                   value="" v-model="username">
                                    

                                                    </div>
                                                    <span class="text-danger">{{ errors[0] }}</span>
                                                    </validation-provider>
                                                    <validation-provider rules="required" v-slot="{ errors }">
                        <div class="input-group mt-3">
                            <div class="input-group-prepend">
                                <span class="input-group-text"><i class="fa fa-lock"></i></span>
                            </div>
                            
                            <input name="password" type="password"
                                   class="form-control"
                                   required
                                   placeholder="Password"
                                   value=""
                                   v-model="password">
                                     

                            </div>
                            <span class="text-danger">{{ errors[0] }}</span>
                            </validation-provider>
                        <div class="input-group mt-4">
                            <div class="form-check checkbox">
                                <input class="form-check-input" name="remember" type="checkbox" id="remember" style="vertical-align: middle;" />
                                <label class="form-check-label" for="remember" style="vertical-align: middle;">
                                    Remember me
                                </label>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-6">
                                <button type="submit" class="btn btn-primary px-4">
                                    Login
                                </button>
                            </div>
                            <div class="col-6 text-right">
                                <a class="btn btn-link px-0" href="/">
                                    Forgot your password?
                                </a>
                                <br><a class="btn btn-link px-0" href="/">
                                    Register
                                </a>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
        </div>
        </div>
        </div>
</template>
<script>
import { ValidationProvider, extend } from 'vee-validate';
import { required } from 'vee-validate/dist/rules';
import axios from 'axios';
extend('required', {
  ...required,
  message: 'This field is required'
});
export default {
    components: {
        ValidationProvider
    },
    data() {
        return {
            username :'',
            password: '',
            loginerror : false
        }
    },
    methods : {
        submitLogin(){
            
            let that = this;
            that.loginerror = false;
            axios.post('http://digitalreinvent.com/login.php',{
                username : that.username,
                password : that.password,
            },{
                headers: {
                    'Content-Type': 'application/json',
                }
            }).then((response)=>{
                this.$router.push('dashboard'); 
            }).catch((errors)=>{
                that.loginerror = true;
            })
        }
    }
};
</script>