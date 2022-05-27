<template>
  <div>
    <h1> {{ event.title }}</h1>
  </div>
</template>

<script>
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
  async asyncData({ $axios, error,params }) {
    try {
      const { data } = await $axios.get("http://localhost:3000/events/" + params.id);
      return {
        event: data,
      };
    } catch (e) {
      error({
        statusCode: 503,
        message: "Unable to fetch event."+ params.id,
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