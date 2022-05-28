<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
import EventService from "../../services/EventService";

export default {
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "What you need to know about" + this.event.id,
        },
      ],
    };
  },
  async asyncData({ error, params }) {
    try {
      const { data } = await EventService.getEvents(params.id);
      return {
        event: data,
      };
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch event." + params.id,
      });
    }
  },
  // computed: {
  //   id() {
  //     return this.$route.params.id;
  //   },
  // },
};
</script>

<style>
</style>