<template>
    <div class="canteen-detail">
      <div class="header2" v-bind:style="{ backgroundImage: 'linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)),  url(' + require('@/assets/images/eat&meat.png') + ')' }">
        <router-link :to="'/'" class="back-button"><img src="@/assets/images/arrow-left.png" alt="back"></router-link>
        <h1>{{ name }}</h1>
      </div>
      
      <div class="canteen-content">
        <Menu 
          :menu="menu"
          :canteen_id="this.$route.params.id"
          @update-menu="updateMenu"
        ></Menu>
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
  data() {
    return {
      menu: {},
      openingHours:{},
      location: '',
      share: '',
      website: '',
      name: ''
    };
  },
  methods: {
    getCanteenDetails() {
      axios.get('https://mupko.pythonanywhere.com/menus/' + this.$route.params.id + '/' + this.getCurrentDate(), {headers: {'Content-Type': 'application/json'}}).then((response) => {
        this.menu = response.data;
      });

      axios.get('https://mupko.pythonanywhere.com/canteens/' + this.$route.params.id, {headers: {'Content-Type': 'application/json'}}).then((response) => {
        this.openingHours = response.data.hours.split(',');
        this.location = response.data.location; // TODO
        this.share = response.data.web; // TODO
        this.website = response.data.web;
        this.name = response.data.name;
      });
    },
    getCurrentDate(){
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth()+1; 
      var yyyy = today.getFullYear();

      if (dd < 10) {
          dd = '0' + dd;
      } 

      if (mm < 10) {
          mm = '0' + mm;
      } 

      today = yyyy + '-' + mm + '-' + dd;
      return today;
    },
    updateMenu(newMenu) {
      this.menu = newMenu;
    },
  },
  mounted() {
    this.getCanteenDetails()
    this.getCurrentDate()
  }
}
</script>
