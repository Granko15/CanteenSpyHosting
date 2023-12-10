<template>
  <Filter></Filter>

  <router-link :to="'/detail/' + canteen.id" v-bind:key="canteen" v-for="canteen in canteens">
    <div class="canteens">
      <Canteen 
        :canteen_id="canteen.id" 
        :name="canteen.name" 
        :stars="4"
        open_until="16:00"
        menu_price="4,10"
        image="eat&meat.png"
        address="Adresa jedálne"
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
      canteens: {}
    }
  },
  methods: {
    getCanteens() {
      axios.get('https://mupko.pythonanywhere.com/canteens/', {headers: {'Content-Type': 'application/json'}}).then((response) => {
        this.canteens = response.data.canteens;
      });
    },
  },
  mounted() {
    this.getCanteens()
  }
}
</script>
