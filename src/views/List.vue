<template>
  <div class="list">
    <Filters />
  </div>
</template>

<script>
// @ is an alias to /src
import Filters from "@/components/Filters.vue";
export default {
  name: "List",
  components: {
    Filters,
  },
};
</script>
