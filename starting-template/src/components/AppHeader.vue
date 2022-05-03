<template>
  <nav class="navbar navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand"
        >Marvel
        <!-- <pre>AppHeader search: {{ search }}</pre> -->
      </a>
      <form class="d-flex">
        <input
          class="form-control me-2"
          type="search"
          placeholder="Поиск..."
          aria-label="Search"
          v-model="search"
          @input="characterSearch(search)"
          @keypress.enter.prevent
        />
        <button
          class="btn btn-outline-success"
          type="submit"
          @click="
            search = '';
            characterSearch(search);
          "
        >
          Все
        </button>
      </form>
    </div>
  </nav>
</template>

<script>
export default {
  name: "AppHeader",
  props: ["characterSearch"],
  data() {
    return {
      search: "",
    };
  },
};
</script>

<style scoped></style>
