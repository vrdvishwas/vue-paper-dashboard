<template>
    <div class="row">
      <div class="col-12">
        <router-link :to="{ name: 'merchant-create'}" class="btn btn-success float-right">Create</router-link>
        <div class="clearfix mb-2"></div>
        <card :title="table1.title" :subTitle="table1.subTitle">
          
          <div slot="raw-content" class="table-responsive">
              <table class="table table-striped">
                <thead>
                    <tr>
                      <th>Merchant ID</th>
                      <th>Name</th>
                      <th>MCC</th>
                      <th>Phone</th>
                      <th>Primary Currency</th>
                      <th>City</th>
                      <th>Active since</th>
                      <th>Status</th>
                      <th></th>
                    </tr>
                </thead>
                <tbody>
                  <tr v-for="(item, index) in merchants" :key="index">
                    <td>{{item.merchant_id}}</td>
                    <td>{{item.name}}</td>
                    <td>{{item.mcc}}</td>
                    <td>{{item.phone}}</td>
                    <td>{{item.primary_currency}}</td>
                    <td>{{item.address.city}}</td>
                    <td>{{item.registered_on}}</td>
                    <td>
                      <label class="switch">
  <input type="checkbox" :checked="item.status=='active'">
  <span class="slider round"></span>
</label>
                    </td>
                    <td>
                      <router-link :to="{ name: 'merchant-edit', params: {merchant_id: item.merchant_id }}" class="text-primary"><i class="fa fa-edit"></i></router-link>
                      | 
                      <router-link :to="{ name: 'merchant-delete', params: {merchant_id: item.merchant_id }}" class="text-danger"><i class="fa fa-times"></i></router-link>
                      
                      </td>
                  </tr>
                </tbody>
              </table>
          </div>
        </card>
      </div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
  data() {
    return {
      merchants : [],
      table1: {
        title: "Merchant",
        subTitle: "---------------",
      },
    };
  },
  mounted() {
      this.loadData();
  },
  methods :{
    loadData(){
      let that = this;
        axios.get('https://digitalreinvent.com/merchant.php')
        .then((response)=>{
          that.merchants = response.data.merchants;
        }).catch((errors)=>{
            console.log(errors);
        })
    }
  }
};
</script>
<style>
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}
.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}
input:checked + .slider {
  background-color: #41B883;
}
input:focus + .slider {
  box-shadow: 0 0 1px #41B883;
}
input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}
/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}
.slider.round:before {
  border-radius: 50%;
}
</style>
