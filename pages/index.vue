/* eslint-disable no-console */
<template>
  <div>
    <v-row align="center" justify="center">
      <v-img
        src="https://cdn.discordapp.com/attachments/703679898400587836/760842866846072842/logo_7.png"
      />
    </v-row>
    <v-row justify="center" class="mt-3 mb-4">
      <v-text-field
        v-model="textSearch"
        hide-details
        label="Filled"
        placeholder="Search Anime"
        filled
        outlined
        dense
        single-line
        class="shrink mx-4"
      />
      <v-btn :color="type === warning ? 'blue' : 'error'" loader @click="searchData()">
        Search
      </v-btn><br><br>
    </v-row>
    <v-card-group columns>
      <v-row justify="center">
        <v-card
          v-for="data in animeData.slice(
            (currentPage - 1) * perPage,
            (currentPage - 1) * perPage + perPage
          )"
          :key="data.mal_id"
          style="width: 450px"
          class="mb-3 ml-4"
        >
          <v-row>
            <v-col md="4" align="center">
              <nuxt-link :to="{ name: 'product-id', params: { id: data } }">
                <v-img :src="data.image_url" />
              </nuxt-link>
              Episode : {{ data.episodes }}
            </v-col>
            <v-col md="8">
              <v-card-body :title="data.title">
                <v-card-text>{{ data.synopsis }}</v-card-text>
              </v-card-body>
            </v-col>
          </v-row>
        </v-card>
      </v-row>
    </v-card-group>
    <div v-if="run == true">
      <div class="text-center">
        <v-pagination v-model="currentPage" :length="6" :total-visible="7" />
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      animeData: '',
      textSearch: '',
      perPage: 9,
      currentPage: 1,
      run: false
    }
  },
  methods: {
    searchData () {
      axios
        .get('https://api.jikan.moe/v3/search/anime?q=' + this.textSearch + '')
        .then((response) => {
          this.animeData = response.data.results
          this.run = true
        })
        .catch((err) => {
          // eslint-disable-next-line no-console
          console.log(err)
        })
    }
  }
}
</script>
<style>
.theme--dark.v-application {
  background-image: url("https://image.freepik.com/free-vector/gradient-geometric-shape-background_78532-307.jpg");
  background-attachment: fixed;
  background-position: 100% 100%;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
