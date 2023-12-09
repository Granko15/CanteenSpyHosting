<template>
    <div class="header2">
      <router-link :to="'/detail/0'" class="back-button"><img src="@/assets/images/arrow-left.png" alt="back"></router-link>
      <h1>eat&meat</h1>
    </div>
    <CommentForm></CommentForm>
    <Alergens></Alergens>
</template>

<script>
import Alergens from './Alergens.vue'
import CommentForm from './CommentForm.vue'

export default {
  name: 'CommentPage',
  components: {
    Alergens,
    CommentForm
  }
}
</script>
