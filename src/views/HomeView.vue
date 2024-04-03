<script>
import { ref, onMounted } from 'vue'
import { supabase } from '@/lib/supabase'

export default {
  setup() {
    const characters = ref([])
    const errorMessage = ref(null)

    const fetchCharacters = async () => {
      try {
        const { data, error } = await supabase.from('gen_characters').select('*')

        if (error) throw error

        characters.value = data
      } catch (err) {
        errorMessage.value = err.message
      }
    }

    onMounted(fetchCharacters)

    return {
      characters,
      errorMessage
    }
  }
}
</script>

<template>
  <h1>Test getting datas!</h1>
  <p v-if="errorMessage">{{ errorMessage }}</p>
  <ul>
    <li v-for="character in characters" :key="character.cha_id">
      {{ character.cha_name }}
    </li>
  </ul>
</template>
