<template>
  <div>
    <h1>Create Event, {{ user.name }}</h1>
    <h4>There are {{ catLength }} catagories in this event!</h4>
    <p v-for="cat in categories" :key="cat">{{ cat }}</p>
  </div>
</template>

<script>
import { mapState, mapGetters } from "vuex";

export default {
  computed: {
    ...mapState(["user", "categories"]),
    ...mapGetters(["catLength"])
  }
};
</script>