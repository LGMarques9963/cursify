<template>
  <v-app id="inspire">
    <app-bar />

    <v-main class="bg-grey-lighten-2">
      <v-container>
        <v-row>
          <template v-for="n in 4" :key="n">
            <v-col
              class="mt-2"
              cols="12"
            >
              <strong>Category {{ n }}</strong>
            </v-col>

            <v-col
              v-for="(video, index) in videos"
              :key="`${n}${index}`"
              cols="6"
              md="2"
            >
              <v-sheet height="150">
                <video-player
                  :title="video.title"
                  :url="video.url"
                  :poster="video.thumbnailUrl	"
                />
              </v-sheet>
            </v-col>
          </template>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  import AppBar from '@/components/AppBar.vue';
  import VideoPlayer from '@/components/VideoPlayer.vue';

  import axios from 'axios'
  export default {
    data: () => ({ 
      drawer: null,
      search: '',
      videos: [],
      loading: false

    }),
    components: { AppBar, VideoPlayer },
    created: function() {
      this.searchVideos()
    },
    methods: {
      searchVideos() {
        // this.loading = true;
        // call axios to fetch data
        axios.get('https://jsonplaceholder.typicode.com/photos')
          .then(response => {
            this.videos = response.data;
            // this.loading = false;
            console.log(this.videos)
            console.log(response)
          })
      }
    }
  }
</script>