<template>
  <div>
    <NavBar/>
    <div class="container">
      <h1>Cars</h1>
      <div class="row">
        <div class="col-6">
          <h5>Car List</h5>
          <ul class="list-group">
            <li class="list-group-item list-group-item-action" v-for="car in cars" :key="car.id" @click="onSelected(car)">
              {{car.brand}} {{car.model}} <span class="float-right">{{car.price}}</span>
            </li>
          </ul>
        </div>
        <div class="col-4">
          <CarView :car="selectedCar" @new="onNewCar" @save="onChanges" @delete="onChanges"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cars: [],
      selectedCar: {}
    }
  },
  methods: {
    async getCars(){
      await this.$axios.get('/api/cars')
      .then((res)=>{
        if(res.status==200){
          this.cars = res.data
        }
      })
    },
    onChanges(){
      this.getCars()
      this.selectedCar = {}
    },
    onSelected(car){
      this.selectedCar = car 
    },
    onNewCar(){
      this.selectedCar = {}
    }
  },
  created() {
    this.getCars()
  }
}
</script>

<style>

</style>