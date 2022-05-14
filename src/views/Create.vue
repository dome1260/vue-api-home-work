<template>
  <div>
    <div class="form__card">
      <label> First name : </label>
      <input type="text" v-model="form.firstname"> <br><br>
      <label> Last name : </label>
      <input type="text" v-model="form.lastname"> <br><br>
      <label> Age : </label>
      <input type="number" v-model="form.age"> <br><br>

      <button @click="submit()"> create </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'CreatePage',
  data () {
    return {
      form: {
        firstname: '',
        lastname: '',
        age: 0,
      },
    }
  },
  methods: {
    async submit () {
      try {
        await axios.post('https://626e332f034ec185d33a2ca2.mockapi.io/customer', {
          firstname: this.form.firstname,
          lastname: this.form.lastname,
          age: this.form.age,
        })
        this.clearForm()
        this.$router.push({ path: '/' })
        alert('create success')

      } catch (error) {
        console.error('[ERROR] create data', error)
      }
    },
    clearForm () {
      this.form = {
        id: null,
        firstname: '',
        lastname: '',
        age: 0,
      }
    },
  }
}
</script>

<style scoped>
  .form__card {
    width: 300px;
    padding: 16px;
    border: 1px solid black;
    margin-bottom: 16px;
  }
</style>
