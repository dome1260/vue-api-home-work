<template>
  <div>
    <div class="form__card">
      <label> First name : </label>
      <input type="text" v-model="form.firstname"> <br><br>
      <label> Last name : </label>
      <input type="text" v-model="form.lastname"> <br><br>
      <label> Age : </label>
      <input type="number" v-model="form.age"> <br><br>

      <button  @click="update()"> update </button>

      <button  @click="back()"> back </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'UpdatePage',
  data () {
    return {
      form: {
        id: null,
        firstname: '',
        lastname: '',
        age: 0,
      },
    }
  },
  mounted () {
    this.loadData()
  },
  methods: {
    async loadData () {
      try {
        const response = await axios.get(`https://626e332f034ec185d33a2ca2.mockapi.io/customer/${this.$route.params.id}`)
        this.form = {
          ...response.data
        }
      } catch (error) {
        console.error('[ERROR] get data', error)
      }
    },
    async update () {
      try {
        await axios.put(`https://626e332f034ec185d33a2ca2.mockapi.io/customer/${this.$route.params.id}`, this.form)
        this.back()
        alert('update success')
      } catch (error) {
        console.error('[ERROR] update data', error)
      }
    },
    back () {
      this.$router.push({ path: '/' })
    }
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
