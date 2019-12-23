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
                      <th>Phone</th>
                      <th>Active since</th>
                      <th>Status</th>
                      <th></th>
                    </tr>
                </thead>
                <tbody>
                  <tr v-for="(item, index) in merchants" :key="index">
                    <td>{{item.merchant_id}}</td>
                    <td>{{item.name}}</td>
                    <td>{{item.phone}}</td>
                    <td>{{item.registered_on}}</td>
                    <td>{{item.status}}</td>
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
        title: "Merchant Groups",
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
        axios.get('http://digitalreinvent.com/merchant.php')
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
</style>
