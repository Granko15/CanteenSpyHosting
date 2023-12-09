<template>
  <Filter></Filter>

  <router-link :to="'/detail/'+item.id" v-bind:key="item" v-for="item in response">
    <div class="canteens">
      <Canteen 
        :canteen_id="item.id" 
        :name="item.name" 
        :stars="item.stars" 
        :open_until="item.open_until"
        :menu_price="item.menu_price"
        :image="item.image"
        :address="item.address"
      ></Canteen>
    </div>
  </router-link>

</template>

<script>
import Filter from './Filter.vue'
import Canteen from './Canteen.vue'
import axios from 'axios'

export default {
  name: 'MainPage',
  components: {
    Filter,
    Canteen
  },
  data() {
    return {
      response: [
        {id: 1, name: "eat&meat", stars: 5, open_until: "20:00", menu_price: "4,10", image: "eat&meat.png", address: "Átriové domky blok AD-U"},
        {id: 2, name: "fayn food", stars: 4, open_until: "16:00", menu_price: "4,30", image: "faynfood.jpg", address: "Fakulta fyziky"},
        {id: 3, name: "prif uk delikanti", stars: 3, open_until: "16:00", menu_price: "5,50", image: "delikanti.png", address: "Prírodovedecká fakulta"},
        {id: 4, name: "free food", stars: 3, open_until: "15:00", menu_price: "4,20", image: "freefood.jpg", address: "Fakulta matematiky"},
        {id: 5, name: "fiit food", stars: 3, open_until: "16:30", menu_price: "4,80", image: "fiitfood.png", address: "Ilkovičova 2, FIIT STU"}
      ]
    }
  },
  methods: {
    getCanteens() {
      axios.get('https://mupko.pythonanywhere.com/canteens/', {headers: {'Content-Type': 'application/json'}}).then((response) => {
        console.log(response);
      });
    },
  },
  mounted() {
    this.getCanteens()
  }
}
</script>
