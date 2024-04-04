<script>
import { ref, onMounted } from 'vue'
import { supabase } from '@/lib/supabase'

export default {
  setup() {
    const characters = ref([])
    const weapons = ref([])
    const artifacts = ref([])
    const errorMessage = ref(null)

    const fetchCharacters = async () => {
      try {
        const { data, error } = await supabase.from('gen_characters').select('*').order('cha_id')

        if (error) {
          console.log('error', error)
        } else {
          console.log('data', data)
        }

        characters.value = data
      } catch (err) {
        errorMessage.value = err.message
      }
    }

    const fetchWeapons = async () => {
      try {
        const { data, error } = await supabase.from('gen_weapons').select('*')

        if (error) {
          console.log('error', error)
        } else {
          console.log('data', data)
        }

        weapons.value = data
      } catch (err) {
        errorMessage.value = err.message
      }
    }

    const fetchArtifacts = async () => {
      try {
        const { data, error } = await supabase.from('gen_artifacts').select('*')

        if (error) {
          console.log('error', error)
        } else {
          console.log('data', data)
        }

        artifacts.value = data
      } catch (err) {
        errorMessage.value = err.message
      }
    }

    onMounted(fetchCharacters)
    onMounted(fetchWeapons)
    onMounted(fetchArtifacts)

    return {
      characters,
      weapons,
      artifacts,
      errorMessage
    }
  }
}
</script>

<template>
  <h1>Test getting datas!</h1>
  <p v-if="errorMessage">{{ errorMessage }}</p>
  <h1>Personnages</h1>
  <ul>
    <li v-for="character in characters" :key="character.cha_id">
      {{ character.cha_name }}
    </li>
  </ul>
  <h1>Artéfacts</h1>
  <ul>
    <li v-for="artifact in artifacts" :key="artifact.art_id">
      {{ artifact.art_label }}
    </li>
  </ul>
  <h1>Weapons</h1>
  <ul>
    <li v-for="weapon in weapons" :key="weapon.wea_id">
      {{ weapon.wea_name }}
    </li>
  </ul>
</template>
