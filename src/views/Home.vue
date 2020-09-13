<template>
  <div class="home">
    <h1>Adopt a new best friend!</h1>
    <h3>Pets in database: {{ animalsCount }}</h3>
    <p>Cats: {{ getAllCats }}</p>
    <p>Dogs: {{ getAllDogs }}</p>
    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>
    <hr />

    <b-jumbotron v-if="showPetForm">
      <b-form @submit.prevent="handleSubmit">
        <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
          <b-form-input id="input-2" v-model="formData.name" required placeholder="Enter name"></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Breed:" label-for="input-3">
          <b-form-input id="input-2" v-model="formData.breed" required placeholder="Enter breed"></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Species:" label-for="input-3">
          <b-form-select
            id="input-3"
            v-model="formData.species"
            :options="['cats', 'dogs']"
            required
          ></b-form-select>
        </b-form-group>

        <b-form-group id="input-group-3" label="Gender:" label-for="input-3">
          <b-form-select
            id="input-3"
            v-model="formData.gender"
            :options="['Male', 'Female']"
            required
          ></b-form-select>
        </b-form-group>

        <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
          <b-form-input id="input-2" v-model="formData.age" required placeholder="Enter age"></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Pet's color:" label-for="input-2">
          <b-form-input id="input-2" v-model="formData.color" required placeholder="Enter color"></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Pet's weight:" label-for="input-2">
          <b-form-input id="input-2" v-model="formData.weight" required placeholder="Enter weight"></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Pet's location:" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="formData.location"
            required
            placeholder="Enter location"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Notes:" label-for="input-2">
          <b-form-input id="input-2" v-model="formData.notes" required placeholder="Enter notes"></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </b-form>
    </b-jumbotron>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        species: null,
        gender: null,
        age: 0,
        breed: '',
        weight: 0,
        location: '',
        notes: ''
      }
    }
  },
  computed: {
    ...mapGetters(['animalsCount', 'getAllCats', 'getAllDogs'])
  },
  methods: {
    ...mapActions(['addPet']),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const {
        species,
        gender,
        age,
        color,
        name,
        breed,
        weight,
        location,
        notes
      } = this.formData
      const payload = {
        species,
        pet: {
          name,
          species,
          age,
          color,
          breed,
          gender,
          weight,
          location,
          notes
        }
      }
      this.addPet(payload)

      // Reset form
      this.formData = {
        name: '',
        species: null,
        gender: null,
        age: 0,
        breed: '',
        weight: 0,
        location: '',
        notes: ''
      }
    }
  }
}
</script>
