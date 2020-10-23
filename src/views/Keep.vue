<template>
  <v-container
    fluid
    fill-height
    class="grey lighten-4">
    <v-row v-masonry>
      <v-col
        v-for="(item, index) in items"
        :key="index"
        cols="12"
        sm="3">
        <v-card
          height="100%"
          color="blue"
          class="pt-1 pb-1"
          @click="deleteItem(index)">
          <v-card-title>{{ item.title }}</v-card-title>
          <v-img
            :src="item.img"
            @load="this.$redrawVueMasonry()"></v-img>
          <v-card-text>{{ item.text }}</v-card-text>
        </v-card>
      </v-col>
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
      items: [
        {
          title: "ha",
          text: "hammad asif"
        },
        {
          title: "ha",
          text: "akjshdlkashdblashbdlasybdlaskbhdkashdbkasdhakshd lahd laskjgdlasjdgals dgaksld alsd lasd akjshdlkashdblashbdlasybdlaskbhdkashdbkasdhakshd lahd laskjgdlasjdgals dgaksld alsd lasd akjshdlkashdblashbdlasybdlaskbhdkashdbkasdhakshd lahd laskjgdlasjdgals dgaksld alsd lasdakjshdlkashdblashbdlasybdlaskbhdkashdbkasdhakshd lahd laskjgdlasjdgals dgaksld alsd lasdakjshdlkashdblashbdlasybdlaskbhdkashdbkasdhakshd lahd laskjgdlasjdgals dgaksld alsd lasd akjshdlkashdblashbdlasybdlaskbhdkashdbkasdhakshd lahd laskjgdlasjdgals dgaksld alsd lasd "
        }
        ,
        {
          title: "ha",
          text: "hammad asif"
        },
        {
          title: "ha",
          text: "hammad asif"
        }
      ]
    }
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
        title: chance.sentence(),
        text: chance.paragraph()
      })
      this.$nextTick(() => {
        this.$redrawVueMasonry()
      })
    }
  }
}
</script>
