<template>
  <div>
    <h3>Top Heroes</h3>
    <div class="grid grid-pad">
      <router-link
        v-for="(hero, index) of heroes"
        :key="index"
        class="col-1-4"
        :to="{ path: `/detail/${hero.id}`}"
      >
        <div class="module hero">
          <h4>{{hero.name}}</h4>
        </div>
      </router-link>
    </div>
    <app-hero-search />
  </div>
</template>

<script>
import { heroService } from './hero.service';
import HeroSearchComponent from './hero-search.vue';

export default {
  name: 'DashboardComponent',
  components: {
    'app-hero-search': HeroSearchComponent
  },
  data: function() {
    return {
      heroes: null
    };
  },
  created() {
    this.getHeroes();
  },
  methods: {
    getHeroes() {
      heroService.getHeroes().then(heroes => (this.heroes = heroes.slice(1, 5)));
    }
  }
};
</script>

<style scoped>
/* DashboardComponent's private CSS styles */
[class*='col-'] {
  float: left;
  padding-right: 20px;
  padding-bottom: 20px;
}
[class*='col-']:last-of-type {
  padding-right: 0;
}
a {
  text-decoration: none;
}
*,
*:after,
*:before {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
h3 {
  text-align: center;
  margin-bottom: 0;
}
h4 {
  position: relative;
}
.grid {
  margin: 0;
}
.col-1-4 {
  width: 25%;
}
.module {
  padding: 20px;
  text-align: center;
  color: #eee;
  max-height: 120px;
  min-width: 120px;
  background-color: #3f525c;
  border-radius: 2px;
}
.module:hover {
  background-color: #eee;
  cursor: pointer;
  color: #607d8b;
}
.grid-pad {
  padding: 10px 0;
}
.grid-pad > [class*='col-']:last-of-type {
  padding-right: 20px;
}
@media (max-width: 600px) {
  .module {
    font-size: 10px;
    max-height: 75px;
  }
}
@media (max-width: 1024px) {
  .grid {
    margin: 0;
  }
  .module {
    min-width: 60px;
  }
}
</style>
