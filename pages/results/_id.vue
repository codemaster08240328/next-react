<template lang="html">
  <div>
    <h1> Results for {{$route.params.id}} </h1>
    <div v-if="albumExists">
      <div v-for="(album, index) in albumData">
        <Card
          :artistName="album.artistName"
          :title="album.collectionCensoredName"
          :image="album.artworkUrl100"
          :color="purple"
        />
      </div>

    {{albumData}}
    </div>
    <div v-else>
      <h3>Could Not Find Album</h3>
    </div>

  </div>
</template>
<script>
import axios from "axios";
import Card from "~/components/Card";

export default {
  asyncData({ params }) {
    return axios
      .get(`https://itunes.apple.com/search?term=${params.id}&entity=album`)
      .then(response => {
        return { albumData: response.data.results };
      });
  },
  components: {
    Card
  },
  middleware: "search",
  computed: {
    albumExists() {
      return this.albumData.length > 0;
    }
  },
  methods: {
    picker(index) {
      return index % 2 == 0 ? "red" : "blue";
    }
  }
};
</script>
