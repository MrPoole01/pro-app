<template>
  <div>
    <h1>Event List</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <template v-if="page != 1">
      <router-link class="nav-b" :to="{ name: 'event-list', query: { page: page -1 }}" rel="prev">
        <i class="fas fa-arrow-left"></i>
      </router-link>
    </template>
    <router-link
      v-if="hasNextPage"
      class="nav-b"
      :to="{ name: 'event-list', query: { page: page +1 }}"
      rel="NEXT"
    >
      <i class="fas fa-arrow-right"></i>
    </router-link>
  </div>
</template>

<script>
import EventCard from "@/components/EventCard.vue";
import { mapState } from "vuex";

export default {
  components: {
    EventCard
  },
  created() {
    this.perPage = 3;
    this.$store.dispatch("fetchEvents", {
      perPage: this.perPage,
      page: this.page
    });
  },
  computed: {
    page() {
      return parseInt(this.$route.query.page) || 1;
    },
    hasNextPage() {
      return this.eventsTotal > this.page * this.perPage;
    },
    ...mapState(["events", "eventsTotal"])
  }
};
</script>

<style lang="scss" scoped>
.nav-b {
  margin: 0 0.5rem 0 0.5rem;
  text-decoration-line: none;
  text-decoration: none;
}
</style>