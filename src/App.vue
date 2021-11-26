<template>
  <div id="content">
    <div id="navigation">
      <div v-for="film in films" @click="showFilmData(film)" v-bind:key="film">
        <div id="film-name">{{ film.title }}</div>
      </div>
    </div>
    <div id="main">
      <input
        id="search"
        v-if="needToSearch"
        v-model="searchString"
        type="text"
      />

      <div id="search-list" v-if="searchString !== ''">
        <div v-for="foundFilm in filteredFilms" v-bind:key="foundFilm">
          {{ foundFilm.title }}
        </div>
        <div v-for="foundPeople in filteredPeople" v-bind:key="foundPeople">
          {{ foundPeople.name }}
        </div>
        <div v-for="foundPlanets in filteredPlanets" v-bind:key="foundPlanets">
          {{ foundPlanets.name }}
        </div>
        <div v-for="foundSpecies in filteredSpecies" v-bind:key="foundSpecies">
          {{ foundSpecies.name }}
        </div>
        <div
          v-for="foundStarships in filteredStarships"
          v-bind:key="foundStarships"
        >
          {{ foundStarships.name }}
        </div>
        <div
          v-for="foundVehicles in filteredVehicles"
          v-bind:key="foundVehicles"
        >
          {{ foundVehicles.name }}
        </div>
      </div>

      <div v-if="Object.keys(filmData).length != 0">
        <div><b>Title: </b>{{ filmData.title }}</div>
        <div>
          <b>Created: </b>{{ new Date(filmData.created).getFullYear() }}-{{
            new Date(filmData.created).getMonth() + 1
          }}-{{ new Date(filmData.created).getDate() }}
        </div>
        <div><b>Director: </b>{{ filmData.director }}</div>
        <div>
          <b>Edited: </b>{{ new Date(filmData.edited).getFullYear() }}-{{
            new Date(filmData.edited).getMonth() + 1
          }}-{{ new Date(filmData.edited).getDate() }}
        </div>
        <div><b>Opening: </b>{{ filmData.opening_crawl }}</div>
        <div><b>Producer: </b>{{ filmData.producer }}</div>
        <div><b>Release: </b>{{ filmData.release_date }}</div>
      </div>
      <div v-if="peopleData.length > 0" class="related-people">
        <b>Characters: </b>
        <div
          id="characters-list"
          v-for="people in peopleData"
          v-bind:key="people.name"
        >
          {{ people.name }}
        </div>
      </div>
      <div v-if="planetsData.length > 0" class="related-people">
        <b>Planets: </b>
        <div
          id="characters-list"
          v-for="planets in planetsData"
          v-bind:key="planets.name"
        >
          {{ planets.name }}
        </div>
      </div>
      <div v-if="speciesData.length > 0" class="related-people">
        <b>Species: </b>
        <div
          id="characters-list"
          v-for="species in speciesData"
          v-bind:key="species.name"
        >
          {{ species.name }}
        </div>
      </div>
      <div v-if="starshipsData.length > 0" class="related-people">
        <b>Starships: </b>
        <div
          id="characters-list"
          v-for="starships in starshipsData"
          v-bind:key="starships.name"
        >
          {{ starships.name }}
        </div>
      </div>
      <div v-if="vehiclesData.length > 0" class="related-people">
        <b>Vehicles: </b>
        <div
          id="characters-list"
          v-for="vehicles in vehiclesData"
          v-bind:key="vehicles.name"
        >
          {{ vehicles.name }}
        </div>
      </div>

      <div id="link-wrap">
        <div v-if="peopleData.length > 0" class="related-people">
          <b>Characters: </b>
          <div
            id="characters-list"
            v-for="people in peopleData"
            v-bind:key="people.name"
          >
            <div id="link-film_person" @click="showPeopleData(people)">
              {{ people.name }}
            </div>
          </div>
        </div>
        <div v-if="planetsData.length > 0" class="related-people">
          <b>Planets: </b>
          <div
            id="characters-list"
            v-for="planets in planetsData"
            v-bind:key="planets.name"
          >
            <div id="link-film_person" @click="showPlanetsData(planets)">
              {{ planets.name }}
            </div>
          </div>
        </div>
        <div v-if="speciesData.length > 0" class="related-people">
          <b>Species: </b>
          <div
            id="characters-list"
            v-for="species in speciesData"
            v-bind:key="species.name"
          >
            <div id="link-film_person" @click="showSpeciesData(species)">
              {{ species.name }}
            </div>
          </div>
        </div>
        <div v-if="starshipsData.length > 0" class="related-people">
          <b>Starships: </b>
          <div
            id="characters-list"
            v-for="starships in starshipsData"
            v-bind:key="starships.name"
          >
            <div id="link-film_person" @click="showStarshipsData(starships)">
              {{ starships.name }}
            </div>
          </div>
        </div>
        <div v-if="vehiclesData.length > 0" class="related-people">
          <b>Vehicles: </b>
          <div
            id="characters-list"
            v-for="vehicles in vehiclesData"
            v-bind:key="vehicles.name"
          >
            <div id="link-film_person" @click="showVehiclesData(vehicles)">
              {{ vehicles.name }}
            </div>
          </div>
        </div>
      </div>

      <div id="film-attribute">
        <div
          v-if="Object.keys(peopleActiveData).length != 0"
          id="attribute-list"
        >
          <b>Character: </b>
          <div>
            <b>Name: </b>
            {{ peopleActiveData.name }}
          </div>
          <div>
            <b>Gender: </b>
            {{ peopleActiveData.gender }}
          </div>
          <div>
            <b>height: </b>
            {{ peopleActiveData.height }}
          </div>
          <div>
            <b>mass: </b>
            {{ peopleActiveData.mass }}
          </div>
          <div>
            <b>Hair color: </b>
            {{ peopleActiveData.hair_color }}
          </div>
        </div>
        <div
          v-if="Object.keys(planetsActiveData).length != 0"
          id="attribute-list"
        >
          <b>Planet: </b>
          <div>
            <b>Name: </b>
            {{ planetsActiveData.name }}
          </div>
          <div>
            <b>Climate: </b>
            {{ planetsActiveData.climate }}
          </div>
          <div>
            <b>Diameter: </b>
            {{ planetsActiveData.diameter }}
          </div>
          <div>
            <b>Orbital period: </b>
            {{ planetsActiveData.orbital_period }}
          </div>
          <div>
            <b>Population: </b>
            {{ planetsActiveData.population }}
          </div>
          <div>
            <b>Terrain: </b>
            {{ planetsActiveData.terrain }}
          </div>
        </div>
        <div
          v-if="Object.keys(speciesActiveData).length != 0"
          id="attribute-list"
        >
          <b>Specie: </b>
          <div>
            <b>Name: </b>
            {{ speciesActiveData.name }}
          </div>
          <div>
            <b>Average height: </b>
            {{ speciesActiveData.average_height }}
          </div>
          <div>
            <b>Average lifespan: </b>
            {{ speciesActiveData.average_lifespan }}
          </div>
          <div>
            <b>Eye colors: </b>
            {{ speciesActiveData.eye_colors }}
          </div>
          <div>
            <b>Language: </b>
            {{ speciesActiveData.language }}
          </div>
          <div>
            <b>Skin colors: </b>
            {{ speciesActiveData.skin_colors }}
          </div>
        </div>
        <div
          v-if="Object.keys(starshipsActiveData).length != 0"
          id="attribute-list"
        >
          <b>Starship: </b>
          <div>
            <b>Name: </b>
            {{ starshipsActiveData.name }}
          </div>
          <div>
            <b>MGLT: </b>
            {{ starshipsActiveData.MGLT }}
          </div>
          <div>
            <b>Cargo capacity: </b>
            {{ starshipsActiveData.cargo_capacity }}
          </div>
          <div>
            <b>Consumables: </b>
            {{ starshipsActiveData.consumables }}
          </div>
          <div>
            <b>Crew: </b>
            {{ starshipsActiveData.crew }}
          </div>
          <div>
            <b>Length: </b>
            {{ starshipsActiveData.length }}
          </div>
          <div>
            <b>Max atmosphering speed: </b>
            {{ starshipsActiveData.max_atmosphering_speed }}
          </div>
          <div>
            <b>Passengers: </b>
            {{ starshipsActiveData.passengers }}
          </div>
        </div>
        <div
          v-if="Object.keys(vehiclesActiveData).length != 0"
          id="attribute-list"
        >
          <b>Vehicle: </b>
          <div>
            <b>Name: </b>
            {{ vehiclesActiveData.name }}
          </div>

          <div>
            <b>Cargo capacity: </b>
            {{ vehiclesActiveData.cargo_capacity }}
          </div>
          <div>
            <b>Consumables: </b>
            {{ vehiclesActiveData.consumables }}
          </div>
          <div>
            <b>Crew: </b>
            {{ vehiclesActiveData.crew }}
          </div>
          <div>
            <b>Length: </b>
            {{ vehiclesActiveData.length }}
          </div>
          <div>
            <b>Max atmosphering speed: </b>
            {{ vehiclesActiveData.max_atmosphering_speed }}
          </div>
          <div>
            <b>Passengers: </b>
            {{ vehiclesActiveData.passengers }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery';

export default {
  name: 'App',
  data() {
    return {
      searchString: '',
      needToSearch: false,
      films: [],
      filmData: {},
      people: [],
      peopleData: [],
      planets: [],
      planetsData: [],
      species: [],
      speciesData: [],
      starships: [],
      starshipsData: [],
      vehicles: [],
      vehiclesData: [],
      peopleActiveData: {},
      planetsActiveData: {},
      speciesActiveData: {},
      starshipsActiveData: {},
      vehiclesActiveData: {},
    };
  },
  computed: {
    filteredFilms() {
      const that = this;
      return that.films.filter((v) => {
        return v.title.toLowerCase().includes(that.searchString.toLowerCase());
      });
    },
    filteredPeople() {
      const that = this;
      return that.people.filter((v) => {
        return v.name.toLowerCase().includes(that.searchString.toLowerCase());
      });
    },
    filteredPlanets() {
      const that = this;
      return that.planets.filter((v) => {
        return v.name.toLowerCase().includes(that.searchString.toLowerCase());
      });
    },
    filteredSpecies() {
      const that = this;
      return that.species.filter((v) => {
        return v.name.toLowerCase().includes(that.searchString.toLowerCase());
      });
    },
    filteredStarships() {
      const that = this;
      return that.starships.filter((v) => {
        return v.name.toLowerCase().includes(that.searchString.toLowerCase());
      });
    },
    filteredVehicles() {
      const that = this;
      return that.vehicles.filter((v) => {
        return v.name.toLowerCase().includes(that.searchString.toLowerCase());
      });
    },
  },
  components: {},
  methods: {
    showFilmData: function (film) {
      this.peopleData = [];
      this.planetsData = [];
      this.speciesData = [];
      this.starshipsData = [];
      this.vehiclesData = [];
      this.filmData = {};

      this.peopleActiveData = {};
      this.planetsActiveData = {};
      this.speciesActiveData = {};
      this.starshipsActiveData = {};
      this.vehiclesActiveData = {};
      var that = this;

      that.filmData = film;
      film.characters.map((char) => {
        that.people.map((p) => {
          char === p.url ? that.peopleData.push(p) : '';
        });
      });
      film.planets.map((pl) => {
        that.planets.map((p) => {
          pl === p.url ? that.planetsData.push(p) : '';
        });
      });
      film.species.map((sp) => {
        that.species.map((p) => {
          sp === p.url ? that.speciesData.push(p) : '';
        });
      });
      film.starships.map((st) => {
        that.starships.map((p) => {
          st === p.url ? that.starshipsData.push(p) : '';
        });
      });
      film.vehicles.map((v) => {
        that.vehicles.map((p) => {
          v === p.url ? that.vehiclesData.push(p) : '';
        });
      });
    },
    showPeopleData: function (people) {
      this.peopleActiveData = {};
      this.planetsActiveData = {};
      this.speciesActiveData = {};
      this.starshipsActiveData = {};
      this.vehiclesActiveData = {};
      const that = this;
      that.peopleActiveData = people;
    },
    showPlanetsData: function (planets) {
      this.peopleActiveData = {};
      this.planetsActiveData = {};
      this.speciesActiveData = {};
      this.starshipsActiveData = {};
      this.vehiclesActiveData = {};
      const that = this;
      that.planetsActiveData = planets;
    },
    showSpeciesData: function (species) {
      this.peopleActiveData = {};
      this.planetsActiveData = {};
      this.speciesActiveData = {};
      this.starshipsActiveData = {};
      this.vehiclesActiveData = {};
      const that = this;
      that.speciesActiveData = species;
    },
    showStarshipsData: function (starships) {
      this.peopleActiveData = {};
      this.planetsActiveData = {};
      this.speciesActiveData = {};
      this.starshipsActiveData = {};
      this.vehiclesActiveData = {};
      const that = this;
      that.starshipsActiveData = starships;
    },
    showVehiclesData: function (vehicles) {
      this.peopleActiveData = {};
      this.planetsActiveData = {};
      this.speciesActiveData = {};
      this.starshipsActiveData = {};
      this.vehiclesActiveData = {};
      const that = this;
      that.vehiclesActiveData = vehicles;
    },
    fetchData: function () {
      this.fetchFilms();
      this.fetchPeople();
      this.fetchPlanets();
      this.fetchSpecies();
      this.fetchStarships();
      this.fetchVehicles();
    },
    fetchPeople: function () {
      var that = this;
      $.ajax({
        url: 'https://swapi.dev/api/people',
        method: 'GET',
        success: function (data) {
          that.people = data.results;
        },
      });
    },
    fetchPlanets: function () {
      var that = this;
      $.ajax({
        url: 'https://swapi.dev/api/planets',
        method: 'GET',
        success: function (data) {
          that.planets = data.results;
        },
      });
    },
    fetchSpecies: function () {
      var that = this;
      $.ajax({
        url: 'https://swapi.dev/api/species',
        method: 'GET',
        success: function (data) {
          that.species = data.results;
        },
      });
    },
    fetchStarships: function () {
      var that = this;
      $.ajax({
        url: 'https://swapi.dev/api/starships',
        method: 'GET',
        success: function (data) {
          that.starships = data.results;
        },
      });
    },
    fetchVehicles: function () {
      var that = this;
      $.ajax({
        url: 'https://swapi.dev/api/vehicles',
        method: 'GET',
        success: function (data) {
          that.vehicles = data.results;
        },
      });
    },
    fetchFilms: function () {
      var that = this;

      $.ajax({
        url: 'https://swapi.dev/api/films',
        method: 'GET',
        success: function (data) {
          that.films = data.results;
          if (that.films.length > 0) {
            that.needToSearch = true;
          }
        },
      });
    },
  },
  beforeMount() {
    this.fetchData();
  },
  watch: {
    filmData: function (newVal) {
      if (Object.keys(newVal).length != 0) {
        const parsed = JSON.stringify(newVal);
        localStorage.setItem('filmData', parsed);
      }
    },
    peopleData: function (newVal) {
      if (Object.keys(newVal).length != 0) {
        const parsed = JSON.stringify(newVal);
        localStorage.setItem('peopleData', parsed);
      }
    },
    planetsData: function (newVal) {
      if (Object.keys(newVal).length != 0) {
        const parsed = JSON.stringify(newVal);
        localStorage.setItem('planetsData', parsed);
      }
    },
    speciesData: function (newVal) {
      if (Object.keys(newVal).length != 0) {
        const parsed = JSON.stringify(newVal);
        localStorage.setItem('speciesData', parsed);
      }
    },
    starshipsData: function (newVal) {
      if (Object.keys(newVal).length != 0) {
        const parsed = JSON.stringify(newVal);
        localStorage.setItem('starshipsData', parsed);
      }
    },
    vehiclesData: function (newVal) {
      if (Object.keys(newVal).length != 0) {
        const parsed = JSON.stringify(newVal);
        localStorage.setItem('vehiclesData', parsed);
      }
    },
    searchString: function (newVal) {
      const parsed = newVal;
      localStorage.setItem('searchString', parsed);
    },
  },
  mounted() {
    if (localStorage.getItem('filmData')) {
      this.filmData = JSON.parse(localStorage.getItem('filmData'));
    }
    if (localStorage.getItem('peopleData')) {
      this.peopleData = JSON.parse(localStorage.getItem('peopleData'));
    }
    if (localStorage.getItem('planetsData')) {
      this.planetsData = JSON.parse(localStorage.getItem('planetsData'));
    }
    if (localStorage.getItem('speciesData')) {
      this.speciesData = JSON.parse(localStorage.getItem('speciesData'));
    }
    if (localStorage.getItem('starshipsData')) {
      this.starshipsData = JSON.parse(localStorage.getItem('starshipsData'));
    }
    if (localStorage.getItem('vehiclesData')) {
      this.vehiclesData = JSON.parse(localStorage.getItem('vehiclesData'));
    }
    if (localStorage.getItem('searchString')) {
      this.searchString = localStorage.getItem('searchString');
    }
  },
};
</script>

<style>
body {
  margin: 0;
}
#content {
  display: flex;
}
#navigation {
  background-color: grey;
  max-height: 100%;
  min-height: 100vh;
  width: 20vw;
}
#main {
  width: 80vw;
  margin-left: 2rem;
}
#film-name {
  cursor: pointer;
}
#film-name:hover {
  color: lawngreen;
}
#film-name:active {
  color: blue;
}
#characters-list {
  margin-left: 6rem;
}
#link-wrap {
  display: flex;
  margin-top: 3rem;
}
#attribute-list {
  margin-top: 3rem;
}
#link-film_person {
  cursor: pointer;
  color: brown;
}
#link-film_person:hover {
  color: blueviolet;
}
#search {
  margin: 1rem 0;
}
#search-list {
  margin-bottom: 1rem;
}
</style>
