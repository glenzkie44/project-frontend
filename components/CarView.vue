<template>
  <div>
    <button class="btn btn-success float-right" @click="onNew">
      New Car
    </button>
    <h5>Car View</h5>
    <hr>

    <form action="" @submit.prevent="">
      <b-form-group label="Brand">
        <b-form-input v-model="car.brand"></b-form-input>
      </b-form-group>
      <b-form-group label="Model">
        <b-form-input v-model="car.model"></b-form-input>
      </b-form-group>
      <b-form-group label="Type">
        <b-form-input v-model="car.type"></b-form-input>
      </b-form-group>
      <b-form-group label="Price">
        <b-form-input type="number" v-model="car.price"></b-form-input>
      </b-form-group>
      <b-form-group label="Date Acquired">
        <b-form-input type="date" v-model="car.acquired_on"></b-form-input>
      </b-form-group>
      <b-form-group>
        <button class="btn btn-primary" @click="onSave">Save Changes</button>
        <button class="btn btn-danger" @click="onDelete" v-if="car.id">Delete</button>
      </b-form-group>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    car: {}
  },
  methods: {
    async onSave(){
      try {
        if(!this.car.id){
          await this.$axios.post('/api/cars', this.car)
        }else{
          await this.$axios.put('/api/cars/' + this.car.id, this.car)
        }

        this.$emit('save')
      }catch(err) {
        alert(err.response.data.message)
      }
    },
    onNew(){
      this.$emit('new')
    },
    async onDelete(){
      try{
        this.$axios.delete('/api/cars/' + this.car.id)
        this.$emit('delete')
      }catch(err){
        alert(err.response.data.message)
      }
    }
  }
}
</script>

<style>

</style>