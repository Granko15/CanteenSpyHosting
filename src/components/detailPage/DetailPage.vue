<template>
    <div class="canteen-detail">
      <div class="header2" v-bind:style="{ backgroundImage: 'linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)),  url(' + require('@/assets/images/' + canteens[this.$route.params.id].image) + ')' }">
        <router-link :to="'/'" class="back-button"><img src="@/assets/images/arrow-left.png" alt="back"></router-link>
        <h1>{{ canteens[this.$route.params.id].name }}</h1>
      </div>
      
      <div class="canteen-content">
        <Menu :menu="menu" @update-menu="updateMenu"></Menu>
        <div class="canteen-contacts">
          <OpeningHours :openingHours="openingHours"></OpeningHours>
          <SocialLinks :location="location" :share="share" :website="website"></SocialLinks>
        </div>
      </div>
    </div>
    
</template>

<script>
import Menu from './Menu.vue';
import OpeningHours from './OpeningHours.vue';
import SocialLinks from './SocialLinks.vue';
import axios from 'axios';

export default {
  name: 'CanteenDetail',
  components: {
    Menu,
    OpeningHours,
    SocialLinks
  },
  props: [
    'canteen_name',
  ],
  methods: {
    getResponse() {
      var menuAPI = 'http://127.0.0.1:8000/menus/' + this.$route.params.id + '/' + this.getCurrentDate();
      console.log(menuAPI);
      axios.get(menuAPI, {headers: {'Content-Type': 'application/json'}}).then((response) => {
        this.menu = response.data;
      })
      axios.get('http://127.0.0.1:8000/canteens/' + this.$route.params.id + '/', {headers: {'Content-Type': 'application/json'}}).then((response) => {
        this.openingHours = response.data.hours.split(',');
        this.location = response.data.location;
        this.share = response.data.web;
        this.website = response.data.web;
      })
    },
    getCurrentDate(){
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth()+1; 
      var yyyy = today.getFullYear();
      if(dd<10) 
      {
          dd='0'+dd;
      } 
      if(mm<10) 
      {
          mm='0'+mm;
      } 
      today = yyyy+'-'+mm+'-'+dd;
      return today;
    },
    updateMenu(newMenu) {
      this.menu = newMenu;
    },
  },
  data() {
    return {
      canteens: [
        {id: 0, name: "eat&meat", stars: 5, open_until: "20:00", menu_price: "4,10", image: "eat&meat.png"},
        {id: 1, name: "fayn food", stars: 4, open_until: "16:00", menu_price: "4,30", image: "faynfood.jpg"},
        {id: 2, name: "prif uk delikanti", stars: 3, open_until: "16:00", menu_price: "5,50", image: "delikanti.png"},
        {id: 3, name: "free food", stars: 3, open_until: "15:00", menu_price: "4,20", image: "freefood.jpg"},
        {id: 4, name: "fiit food", stars: 3, open_until: "16:30", menu_price: "4,80", image: "fiitfood.png"}
      ],
      menu: {},
      openingHours:{},
      location: String,
      share: String,
      website: String
    };
  },
  mounted() {
    this.getResponse()
    this.getCurrentDate()
  }
}
</script>
