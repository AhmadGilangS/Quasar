<template>
  <q-page class="flex flex-center">
      <div class="q-pa-md">
    <q-table
      title="Data Project"
      :data="data"
      :columns="columns"
      row-key="name"
      dark
      color="amber"
    />
  </div>
  </q-page>
 
</template>

<style>
</style>

<script>
import Vue from 'vue'
import Project from "../API/project/index"
export default {
  data () {
    return {
      columns: [
        {
          name: 'ID',
          required: true,
          label: 'ID Project',
          align: 'left',
          field: row => row.id,
          sortable: true
        },
        {
          name: 'capacity',
          required: true,
          label: 'Capacity Person',
          align: 'left',
          field: row => row.capacity,
          sortable: true
        },
        {
          name: 'status',
          required: true,
          label: 'Project Status',
          align: 'left',
          field: row => row.status,
          sortable: true
        },
        {
          name: 'Payment',
          required: true,
          label: 'Payment Status',
          align: 'left',
          field: row => row.paymentStatus,
          sortable: true
        },
        {
          name: 'create At',
          required: true,
          label: 'Timestamps',
          align: 'left',
          field: row => row.createAt,
          sortable: true
        },
        
        
      ],
      data: []
    }
  },

  beforeCreate(){
      let self = this

      Project.getAllProject(window).then(function(datas){
          return datas
      }).then(function(res){
          console.log(res)
          self.data = res
      }).catch(function(err){
          console.log(err)
      })
  }
}
</script>
