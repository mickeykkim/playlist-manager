<template>
  <panel title="Song Details">
    <v-layout>
      <v-flex xs6>
        <div class="song-title">
          {{song.title}}
        </div>
        <div class="song-artist">
          {{song.artist}}
        </div>
        <div class="song-album">
          {{song.album}}
        </div>
        <div class="song-genre">
          {{song.genre}}
        </div>
        <br>
        <div class="song-sharer">
          Shared by: {{song.sharedBy}}
          <br>
        </div>
        <v-btn
          v-if="isUserLoggedIn"
          dark
          class="light-blue darken-1"
          :to="{
            name: 'song-edit',
            params () {
              return {
                songId: song.id
              }
            }
          }">
          <v-icon dark left>edit</v-icon>
          Edit
        </v-btn>
      </v-flex>
      <v-flex xs6>
        <img class="album-image" :src="song.albumImageUrl" />
        <br>
        {{song.album}}
      </v-flex>
    </v-layout>
  </panel>
</template>

<script>
import {mapState} from 'vuex'
export default {
  props: [
    'song'
  ],
  data () {
    return {
      bookmark: null
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user'
    ])
  },
  watch: {
  },
  methods: {
  },
  async mounted () {
  }
}
</script>

<style scoped>
.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}

.song-title {
  font-size: 30px;
}

.song-artist {
  font-size: 24px;
}

.song-album {
  font-size: 18px;
}

.song-genre {
  font-size: 18px;
}

.song-sharer {
  font-size: 20px;
}

.album-image {
  width: 100%;
  margin: 0 auto;
}
</style>
