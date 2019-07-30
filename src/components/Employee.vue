<template>
  <q-page class="flex flex-center">
        <p>{{employeeData}}</p>

        <div class = "row">
            <div class="col-sm-6">
                <p>Ini FirstName</p>
                <button class= "primary" @click="getFirstNameOnly()">FirstName</button>
            </div>
            <div>
            <p>{{firstNameDataOnly}}</p>
            </div>
        </div>

        <div class = "row">
            <div class="col-sm-6">
                <p>Ini LastName</p>
                <button class= "primary" @click="getLastNameOnly()">LastName</button>
            </div>
            <div>
            <p>{{lastNameDataOnly}}</p>
            </div>
        </div>

        <button class= "primary" @click="createNewEmployee()">Submit</button>
  </q-page>
</template>

<style>
</style>

<script>

import Employee from "../API/employee/index"
export default {
  name: 'Employee',

  data(){
      return{
          employeeData:{},
          firstNameDataOnly:[],
          lastNameDataOnly:[],
          param:
              {
                "first_name": "Mie",
                "last_name": "Ayam",
                "email_address": "MieAyam@enak.com",
                "phone": "8370198725"
        }
      }

    },

    methods:{

        getFirstNameOnly(){
            const self = this;
            Employee.getEmployee(window).then(function(datas){
                console.log('ini data nama depan', datas)
                for(let i=0; i<datas.length; i++){
                    self.firstNameDataOnly.push(datas[i].first_name)
                }
                return datas;
            }).catch(function(err){
                console.log(err)
            })
        },

        getLastNameOnly(){
            const self = this;
            Employee.getEmployee(window).then(function(datas){
                console.log('ini data nama belakang', datas)
                for(let i=0; i<datas.length; i++){
                    self.lastNameDataOnly.push(datas[i].last_name)
                }
                return datas;
            }).catch(function(err){
                console.log(err)
            })
        },

        createNewEmployee(){
            const self = this;
            Employee.submitNewEmployee(window, self.param).then(function(result){
               return result;
            }).catch(function(err){
                console.log(err)
            })
        }
    },


  beforeCreate(){
      let self = this

      Employee.getEmployee(window).then(function(datas){
          return datas
      }).then(function(res){
          console.log(res)
          self.employeeData=res
      }).catch(function(err){
          console.log(err)
      })
  }
}
</script>
