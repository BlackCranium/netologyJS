<template>
  <div id="app">
    <app-header :characterSearch="characterSearch" />

    <div class="container">
      <h1 class="pt-3 pb-3">Персонажи Marvel</h1>

      <!-- <pre>characters: {{characters}}</pre> -->
      <!-- <pre>characterIndex: {{characterIndex}}</pre> -->
      <!-- <pre>App search: {{ search }}</pre> -->

      <app-modal :character="filterCharacters[characterIndex]" />

      <spinner v-if="loading" />

      <div class="row">
        <div
          v-for="(el, idx) in filterCharacters"
          v-bind:key="el.id"
          class="card mb-3"
          style="max-width: 440px"
        >
          <div class="row g-0">
            <div class="col-md-4">
              <img
                v-bind:src="el.thumbnail"
                class="img-fluid rounded-start"
                v-bind:alt="el.nameor"
              />
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">{{ el.name }}</h5>

                <!-- Button trigger modal -->
                <button
                  type="button"
                  class="btn btn-primary"
                  data-bs-toggle="modal"
                  data-bs-target="#exampleModal"
                  @click="characterIndex = idx"
                >
                  Подробнее
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Spinner from "./components/Spinner";
import AppModal from "./components/AppModal";
import AppHeader from "./components/AppHeader";

export default {
  name: "App",
  components: {
    AppHeader,
    AppModal,
    Spinner,
  },
  data() {
    return {
      loading: false,
      characters: [],
      characterIndex: 0,
      search: "",
    };
  },
  methods: {
    //https://netology-api-marvel.herokuapp.com/characters
    fetchCharacters: function () {
      return fetch("https://netology-api-marvel.herokuapp.com/characters")
        .then((res) => res.json())
        .then((json) => (this.characters = json));
    },
    characterSearch: function (value) {
      this.search = value;
    },
  },
  computed: {
    filterCharacters: function () {
      //   let characters = this.characters;
      //   let search = this.search;
      let { search, characters } = this;
      return characters.filter((character) => {
        return (
          character.name.toLowerCase().indexOf(search.toLowerCase()) !== -1
        );
      });
    },
  },
  async mounted() {
    this.loading = true;
    await this.fetchCharacters();
    this.loading = false;
  },
};
</script>

<style></style>
