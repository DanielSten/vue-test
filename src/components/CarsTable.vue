<template>
  <div class="wrapper">
    <div class="row my-3">
      <div class="col">
        <b-form-input v-model="id" placeholder="ID"></b-form-input>
      </div>
      <div class="col">
        <b-form-input v-model="brand" placeholder="Brand"></b-form-input>
      </div>
      <div class="col">
        <b-form-input v-model="yearStart" placeholder="Year from"></b-form-input>
      </div>
      <div class="col">
        <b-form-input v-model="yearEnd" placeholder="Year to"></b-form-input>
      </div>
    </div>
    <b-table striped hover :items="filteredData" :fields="fields" :no-local-sorting="true" @sort-changed="sortingChanged" sort-icon-left></b-table>
  </div>
</template>

<script>
import Axios from "axios";

export default {
  name: 'CarsTable',
  props: {
  },
  data(){
    return{
      id: '',
      brand: '',
      yearStart: '',
      yearEnd: '',
      fields: [
        {
          key: 'id',
          label: 'ID',
          sortable: true,
        },
        {
          key: 'brand',
          label: 'Brand',
          sortable: true,
        },
        {
          key: 'age',
          label: 'Year of manufacture',
          sortable: true,
        }
      ],
      cars: [
        {
          id: 1,
          brand: 'BMW',
          age: 2010
        },
        {
          id: 2,
          brand: 'Audi',
          age: 2012
        },
        {
          id: 3,
          brand: 'BMW',
          age: 2016
        },
        {
          id: 4,
          brand: 'Audi',
          age: 2018
        },
      ]
    }
  },
  methods: {
    sortingChanged({sortBy, sortDesc}){
      if(sortDesc){
        sortBy = '-' + sortBy
      }
      Axios.get('https://localhost:3005/cars/index?sort=' + sortBy)
          .then(response => {
            console.log(response)
          })
          .catch(e => console.error(e));
    }
  },
  computed: {
    filteredData() {

      return this.cars.filter(el => {
        if(this.id !== '' && this.id != el.id){
          return false
        }
        if(this.brand !== '' && !el.brand.toLowerCase().includes(this.brand.toLowerCase())){
          return false
        }
        if(this.yearStart !== '' && this.yearStart > el.age){
          return false
        }
        if(this.yearEnd !== '' && this.yearEnd < el.age){
          return false
        }
        return true
      })

    }
  },
}
</script>


<style scoped>
.wrapper{
  max-width: 980px;
  margin: 0 auto;
}

</style>
