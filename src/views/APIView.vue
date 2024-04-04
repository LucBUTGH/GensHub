<template>
  <h1>Getting datas from localhost api</h1>
  <div v-for="item in items" :key="item.char_id">
    <p>{{ item.cha_name }}</p>
  </div>
  <p v-if="error">Erreur lors de la récupération des données: {{ error }}</p>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      items: [],
      error: ''
    }
  },
  async created() {
    try {
      const response = await axios.get('http://127.0.0.1:8000/api/characters')
      this.items = response.data.data
    } catch (error) {
      this.error = error.toString()
    }
  }
}
</script>
