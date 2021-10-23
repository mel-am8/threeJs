<template>
  <sample />
</template>

<script lang="ts">
import Vue from "vue";
import Sample from "../components/Sample.vue";

export default Vue.extend({
  name: "Home",

  components: {
    Sample,
  },
});
</script>
