<template>
  <v-container
    fluid
    fill-height
    class="grey lighten-4">
    <v-row>
      <masonry
        style="width:100%"
        :gutter="{ default: '30px', 700: '15px' }"
        :cols="{ default: 3, 1000: 3, 700: 2, 500: 1 }">
        <v-card
          v-for="item in items"
          :key="item.id"
          class="mt-2 mb-2"
          color="yellow lighten-5">
          <v-toolbar
            flat
            dense
            color="transparent"
            class="font-weight-bold">
            {{ item.title }}
          </v-toolbar>
          <v-img
            v-if="item.img"
            width="100%"
            :height="item.height"
            :src="item.img"></v-img>
          <v-card-text v-if="item.text">
            {{ item.text }}
          </v-card-text>
        </v-card>
      </masonry>
    </v-row>
    <v-btn @click="addNew">
      Add new card
    </v-btn>
  </v-container>
</template>

<script>
const chance = require("chance")()
export default {
  data: function () {
    return {
      items: []
    }
  },
  mounted () {
    Array(20).fill(1).forEach((a) => this.addNew())
  },
  methods: {
    deleteItem (index) {
      this.items.splice(index, 1)
      this.$nextTick(() => {
        this.$redrawVueMasonry()
      })
    },
    addNew () {
      this.items.push({
        id: chance.guid(),
        title: chance.sentence(),
        height: this.items.length % 2 === 0 ? 400 : 800,
        img: this.items.length % 4 === 0 ? `https://picsum.photos/seed/${chance.integer()}/200/200` : undefined,
        text: this.items.length % 4 !== 0 ? chance.paragraph() : undefined
      })
      this.$nextTick(() => {
        this.$redrawVueMasonry()
      })
    }
  }
}
</script>
