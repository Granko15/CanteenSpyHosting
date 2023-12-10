<template>
    <div class="header2">
      <router-link :to="'/detail/' + this.$route.params.canteen_id" class="back-button"><img src="@/assets/images/arrow-left.png" alt="back"></router-link>
      <h1>eat&meat</h1>
    </div>
    <CommentForm
      :comments="comments"
      :name="name"
      :price="price"
    ></CommentForm>
    <Alergens></Alergens>
</template>

<script>
import Alergens from './Alergens.vue'
import CommentForm from './CommentForm.vue'
import moment from 'moment'
import axios from 'axios'

export default {
  name: 'CommentPage',
  components: {
    Alergens,
    CommentForm
  },
  data() {
    return {
      comments: {},
      name: '',
      price: ''
    }
  },
  methods: {
    getComments() {
        axios.get('https://mupko.pythonanywhere.com/ratings/' + this.$route.params.menu_id, {headers: {'Content-Type': 'application/json'}}).then((response) => {
        this.comments = response.data;
        this.comments.forEach(el => {
            el.created_at = moment(String(el.created_at)).format('DD.MM.YYYY HH:mm')
        });
      });
    },
    getMenuDetail() {
      // TODO
      this.name = 'Názov menu';
      this.price = '4,10';
    }
  },
  mounted() {
    this.getComments()
    this.getMenuDetail()
  }
}
</script>
