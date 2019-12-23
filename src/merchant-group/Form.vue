<template>
  <div class="card mx-4">
    <div class="card-body p-4">
      <h3 class="text-muted">Create Merchant</h3>
      <form method="POST" action=""  v-on:submit.prevent="submitMerchantForm">
        <div class="row">
          <div class="col-sm-6">

            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="text" name="merchant[name]" class="form-control" required autofocus placeholder="Name" value="" v-model="merchant.name">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="number" name="merchant[merchant_id]" class="form-control" required placeholder="Merchant Id" value="" min="0" v-model="merchant.merchant_id">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>

<validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="text" name="merchant[mcc]" class="form-control" required placeholder="MCC" value="" model="merchant.mcc">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <select class="form-control" name="merchant[primary_currency]" v-model="merchant.primary_currency">
                <option value="">Currency</option>
                <option value="USD">USD</option>
                <option value="Euro">Euro</option>
              </select>
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <select class="form-control" name="merchant[status]" v-model="merchant.status">
                <option value="">status</option>
                <option value="active">Active</option>
                <option value="inactive">In-active</option>
              </select>
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-4">
              <input type="tel" name="merchant[phone]" class="form-control" required placeholder="phone" v-model="merchant.phone">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>


          </div>
          <div class="col-sm-6">
              <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="text" name="merchant[address][address_line1]" class="form-control" required placeholder="Address Line " v-model="merchant.address.address_line1">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="text" name="merchant[address][city]" class="form-control" required placeholder="city" v-model="merchant.address.city">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="text" name="merchant[address][state]" class="form-control" required placeholder="state" v-model="merchant.address.state">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="text" name="merchant[address][country]" class="form-control" required placeholder="country" v-model="merchant.address.country">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <validation-provider rules="required" v-slot="{ errors }">
            <div class="input-group mb-3">
              <input type="text" name="merchant[address][zip]" class="form-control" required placeholder="zip" v-model="merchant.address.zip">
            </div>
            <span class="text-danger">{{ errors[0] }}</span>
              </validation-provider>
            <button class="btn btn-block btn-primary" type="submit">Create</button>
          </div>
        </div>

      </form>
    </div>

  </div>

</template>
<script>
  import {
    ValidationProvider,
    extend
  } from 'vee-validate';
  import {
    required
  } from 'vee-validate/dist/rules';
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
        submiterror: false,
        merchant: {
          name: "",
          merchant_id: "",
          mcc: "",
          primary_currency: "",
          status: "",
          phone: "",
          registered_on: "2019-12-20 15:30:24",
          address: {
            address_line1: "",
            city: "",
            state: "",
            country: "",
            zip: ""
          }
        }
      };
    },
    methods: {
      submitMerchantForm() {
          
        let that = this;
        that.submiterror = false;
        console.log(that.merchant);
        axios.post('http://digitalreinvent.com/merchant-create.php', that.merchant, {
          headers: {
            'Content-Type': 'application/json',
          }
        }).then((response) => {
          this.$router.push('/merchants');
        }).catch((errors) => {
          that.submiterror = true;
        })
      }
    }
  };

</script>
<style>
</style>
