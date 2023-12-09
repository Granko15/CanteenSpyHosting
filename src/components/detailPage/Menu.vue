<template>
    <div class="menu-box">
        <div class="pagination">
            <img class="nav-arrow" src="../../assets/images/left_arrow.svg" alt="Previous Day" @click="previousDay" :disabled="currentDayIndex === 0" >

            <div class="menu-date">
                <h3>{{ currentDay }}</h3>
                <p>{{ this.formatDate(currentDate) }}</p>
            </div>

            <img class="nav-arrow" src="../../assets/images/right_arrow.svg" alt="Previous Day" @click="nextDay" :disabled="currentDayIndex === days.length - 1">
        </div>
        <div class="menu-items">
                <MenuItem v-for="item in this.menu" 
                v-bind:key="item.id" :id="item.id" :name="item.name" :price="item.price"
                :menu_date="item.day" :meat="item.meat" :vegetarian="item.vegetarian"
                :available="item.available" :unavailable="item.unavailable"
                />
        </div>
    </div>

</template>

<script>
import MenuItem from './MenuItem.vue';
import axios from 'axios';

export default {
    name: 'Menu',
    components: {
        MenuItem
    },
    props: [
        'menu',
    ],
    data() {
        return {
            days: ['Pondelok', 'Utorok', 'Streda', 'Štvrtok', 'Piatok','Sobota', 'Nedeľa'],
            currentDayIndex: new Date().getDay()-1,
            currentDate: this.getCurrentDate(),
        };
    },
    computed: {
        currentDay() {
            return this.days[this.currentDayIndex];
        }
    },
    methods: {
        getMenuItemsByDay(day) {
            return this.menu[day];
        },
        previousDay() {
            if (this.currentDayIndex > 0) {
                this.currentDayIndex--;
                this.decrementDate();
                var menuAPI = 'http://127.0.0.1:8000/menus/' + this.$route.params.id + '/'+ this.formatDateForAPI(this.currentDate);
                axios.get(menuAPI, {headers: {'Content-Type': 'application/json'}}).then((response) => {
                    this.$emit('update-menu', response.data);
                })
            }
        },
        nextDay() {
            if (this.currentDayIndex < this.days.length - 1) {
                this.currentDayIndex++;
                this.incrementDate();
                axios.get('http://127.0.0.1:8000/menus/' + this.$route.params.id + '/' + this.formatDateForAPI(this.currentDate), {headers: {'Content-Type': 'application/json'}}).then((response) => {
                    this.$emit('update-menu', response.data);
                })
            }
        },
        getCurrentDate(){
            var today = new Date();
            return today;
        },
        formatDate(date) {
            var dd = date.getDate();
            var mm = date.getMonth()+1; 
            var yyyy = date.getFullYear();
            return dd+'.'+mm+'.'+yyyy;
        },
        formatDateForAPI(date) {
            var dd = date.getDate();
            var mm = date.getMonth()+1; 
            var yyyy = date.getFullYear();
            return yyyy+'-'+mm+'-'+dd;
        },
        incrementDate() {
            this.currentDate.setDate(this.currentDate.getDate() + 1);
        },
        decrementDate() {
            this.currentDate.setDate(this.currentDate.getDate() - 1);
        }
    }
};
</script>
