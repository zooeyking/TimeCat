<template lang="html">
  <div class="detail">
    <info v-if="detail.themeid == 'info' " :info="detail"></info>
    <music v-if="detail.themeid == 'music' " :info="detail"></music>
    <v-article v-if="detail.themeid == 'article' " :info="detail"></v-article>
    <trip v-if="detail.themeid == 'trip' " :info="detail"></trip>
  </div>
</template>

<script>
import axios from 'axios'
import Info from 'components/info/Info.vue'
import Music from 'components/music/Music.vue'
import Article from 'components/article/Article.vue'
import Trip from 'components/trip/Trip.vue'

const ERR_OK = 0

export default {
  data () {
    return {
      detail:{}
    }
  },
  components: {
    "info": Info,
    "music": Music,
    "v-article": Article,
    "trip": Trip,
  },
  created () {
    axios.get('/api/detail',{
      params: {
        id: this.$route.params
      }
    }).then((res) => {
      res = res.data
      if (res.errno === ERR_OK) {
        this.detail = res.data
      }
    }).catch((error) => {
      console.warn(error)
    })

  }
}
</script>

<style lang="css">
</style>
