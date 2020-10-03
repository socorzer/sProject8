<template>
  <div class="mt-10">
    <v-card align="center" justify="center">
      <v-row>
        <v-col md="4">
          <v-img :src="this.$route.params.id.image_url" />
        </v-col>
        <v-col md="8">
          <h1>{{ this.$route.params.id.title }}</h1>
          <div align="left">
            <h3>---------- {{ this.$route.params.id.synopsis }}</h3>
            <h3>Episode : {{ this.$route.params.id.episodes }}</h3>
            <h3>Score : {{ this.$route.params.id.score }} / 10</h3>
            <h3>Rated : {{ this.$route.params.id.rated }}</h3>
            <h3>Start Date : {{ this.$route.params.id.start_date }}</h3>
            <h3>End Date : {{ this.$route.params.id.end_date }}</h3>
            <a
              style="text-decoration: none;"
              target="_blank"
              :href="this.$route.params.id.url"
            >
              <h3>Ref : {{ this.$route.params.id.url }}</h3>
            </a>
          </div>
        </v-col>
      </v-row>
    </v-card>
  </div>
</template>
