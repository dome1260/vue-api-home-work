<template>
  <div>
    <button @click="goCreate()"> Create </button>
    <table id="customers">
      <thead>
        <tr>
          <th> No </th>
          <th> First Name </th>
          <th> Last Name </th>
          <th> Age </th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, i) in items" :key="i">
          <td>
            {{ i + 1 }}
          </td>
          <td> {{ item.firstname }} </td>
          <td> {{ item.lastname }} </td>
          <td> {{ item.age }} </td>
          <td>
            <button @click="goUpdate(item)"> Edit </button>
            <button @click="deleteData(item.id)"> Delete </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HomePage',
  data () {
    return {
      items: []
    }
  },
  mounted () {
    this.loadData()
  },
  methods: {
    async loadData () {
      try {
        const response = await axios.get('https://626e332f034ec185d33a2ca2.mockapi.io/customer')
        this.items = response.data

      } catch (error) {
        console.error('[ERROR] get data', error)
      }
    },
    async deleteData (id) {
      try {
        await axios.delete(`https://626e332f034ec185d33a2ca2.mockapi.io/customer/${id}`)
        this.loadData()
        alert('delete succuess')
      } catch (error) {
        console.error('[ERROR] delete data', error)
      }
    },
    goCreate () {
      this.$router.push({ name: 'Create' })
    },
    goUpdate (item) {
      this.$router.push({ name: 'Edit', params: { id: item.id } })
    }
  }
}
</script>

<style scoped>
  #customers {
    font-family: Arial, Helvetica, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }

  #customers td, #customers th {
    border: 1px solid #ddd;
    padding: 8px;
  }

  #customers tr:nth-child(even){background-color: #f2f2f2;}

  #customers tr:hover {background-color: #ddd;}

  #customers th {
    padding-top: 12px;
    padding-bottom: 12px;
    text-align: left;
    background-color: #04AA6D;
    color: white;
  }
</style>
