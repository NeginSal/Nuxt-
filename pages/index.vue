<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from "../components/EventCard.vue";
import { mapState } from "vuex";

export default {
  components: {
    EventCard,
  },

  head() {
    return {
      title: "Event Listening",
    };
  },

  // asyncData({ $axios, error }) {
  //   return $axios
  //     .get("http://localhost:3000/events")
  //     .then((response) => {
  //       return {
  //         events: response.data,
  //       };
  //     })
  //     .catch((e) => {
  //       error({
  //         statusCode: 503,
  //         message: "Unable to fetch events at this time . Please try again.",
  //       });
  //     });
  // },

  // async asyncData({ error }) {
  //   try {
  //     const { data } = await EventService.getEvents();
  //     return {
  //       events: data,
  //     };
  //   } catch (e) {
  //     error({
  //       statusCode: 503,
  //       message: "Unable to fetch events at this time . Please try again.",
  //     });
  //   }
  // },

  async fetch({ store, error }) {
    try {
      await store.dispatch("events/fetchEvents");
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch events at this time. Please try again.",
      });
    }
  },
  computed: mapState({
    events: (state) => state.events.events,
  }),
};
</script>

<style>
</style>