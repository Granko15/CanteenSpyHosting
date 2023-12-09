<template>
    <div class="comments-form-box">
        <h3>{{ menus[this.$route.params.id].name }}</h3>
        <p>{{ menus[this.$route.params.id].price }}€</p>
        <div class="comments-box">
            <h3>Komentáre</h3>
            <div class="comments-scroll">
                <div class="comment-box" v-bind:key="item" v-for="item in response">
                    <p>{{ item.comment }}</p>
                    <div class="message-flex">
                        <star-rating 
                            :rating="item.rating"
                            :readonly="true"
                            :star-size="15"
                            active-color="#FFC700"
                            inactive-color="#FFFFFF"
                            border-color="#000000"
                            :border-width="1"
                            :show-rating="false"
                            :star-points="[23,2, 14,17, 0,19, 10,34, 7,50, 23,43, 38,50, 36,34, 46,19, 31,17]">
                        </star-rating>
                        <em>{{ item.date }}</em>
                    </div>
                    <div class="arrow"></div>
                </div>
            </div>
        </div>
        <div class="stars-input">
            <star-rating 
                v-model:rating="rating"
                :star-size="40"
                active-color="#FFC700"
                inactive-color="#E3E3E3"
                border-color="#000000"
                :border-width="1"
                :padding="5"
                :show-rating="false"
                :star-points="[23,2, 14,17, 0,19, 10,34, 7,50, 23,43, 38,50, 36,34, 46,19, 31,17]">
            </star-rating>
        </div>
        <textarea v-model="comment" class="comment-input" placeholder="Napísať hodnotenie" rows="5"></textarea>
        <button v-on:click="submitComment" type="button" class="comment-submit">Odoslať</button>
    </div>
</template>

<script>
import StarRating from 'vue-star-rating'

export default {
  name: 'CommentForm',
  components: {
    StarRating
  },
  props: [
    'menu_id',
    'name',
    'price',
  ],
  data() {
    return {
        rating: 3,
        comment: "",
        response: [
            {rating: 4, comment: "Dobre dochutené, odporúčam!", date: "15.12.2023 12:23"},
            {rating: 5, comment: "Dnes sa podarilo pani kuchárkam :)", date: "15.12.2023 12:33"}
        ],
        menus:[ { id: 0, name: "Frankfurtsk\u00e1 s p\u00e1rkom (1,6)", price: "0.80",day: "2023-12-04",available: 13, unavailable: 1, meat: true,vegetarian: false, canteen_id: 1, rating: 4},
              { id: 1, name: "Toscana so syrom (1,7,9)",price: "0.80",day: "2023-12-04",available: 6,unavailable: 22,meat: false,vegetarian: true, canteen_id: 1,rating: 4 },
              { id: 2, name: "Kuracie prsia s baby karotkou a brokolicou",price: "4.10",day: "2023-12-04",available: 19,unavailable: 7,meat: true,vegetarian: false, canteen_id: 1,rating: 4 },
              { id: 3, name: "Mor\u010dacie sot\u00e9 s nivovou om\u00e1\u010dkou (1,7)",price: "4.10",day: "2023-12-04",available: 30,unavailable: 3,meat: true,vegetarian: false, canteen_id: 1,rating: 4 },
              { id: 4, name: "Seged\u00ednsky gul\u00e1\u0161 (1,7)",price: "4.10",day: "2023-12-04",available: 19,unavailable: 7,meat: true,vegetarian: false, canteen_id: 1,rating: 4 },
          ]
    }
  },
  methods: {
    submitComment() {
        if (this.comment != "") {
            this.response.push({rating: this.rating, comment: this.comment, date: "15.12.2023 12:46"});
        }
        this.rating = 3;
        this.comment = "";
    },
    getComments() {
    }
  },
  mounted() {
    //this.getComments();
  }
}
</script>
