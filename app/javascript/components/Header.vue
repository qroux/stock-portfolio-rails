<template>
<div>
  <nav class="navbar navbar-expand-lg navbar-light bg-light px-4">
    <router-link to='/' activeClass="active navbar-brand"><a>Stock Trader</a></router-link>
    <button class="navbar-toggler" type="button">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <router-link tag="li" to='/portfolio' activeClass="active"><a class="nav-link">Portfolio</a></router-link>
        <router-link tag="li" to='/stocks' activeClass="active"><a class="nav-link">Stocks</a></router-link>
      </ul>
      <ul class="navbar-nav">
        <router-link tag="li" to='/signup' activeClass="active"><a class="nav-link">Sign Up</a></router-link>
        <li class="nav-item mr-2">
          <a id='end' class="nav-link" @click="endDay">End Day</a>
        </li>
        <li class="nav-item dropdown mr-2">
          <a
            class="nav-link dropdown-toggle"
            id="navbarDropdown"
            role="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
            @mouseover="openDropdown = true"
            >
            Save & Load
          </a>
          <div class="dropdown-menu"
          aria-labelledby="navbarDropdown"
          :class="{show: openDropdown}"
          @mouseover="openDropdown = true"
          @mouseout="openDropdown = false"
          >

            <li><a class="dropdown-item" @click="saveData">Save Data</a></li>
            <li><a class="dropdown-item" @click="loadData">Load Data</a></li>
            <div class="dropdown-divider"></div>
            <li><a class="dropdown-item" href="#">Something else here</a></li>
          </div>
        </li>
        <li class="navbar-text"><strong>Funds: {{ funds | currency }}</strong></li>
      </ul>
    </div>
  </nav>
</div>
</template>

<script>
  import {mapActions} from 'vuex'

  export default {
    data() {
      return {
        openDropdown: false
      }
    },
    computed: {
      funds() {
        return this.$store.getters.funds
        }
      },
      methods: {
        ...mapActions({
          randomizeStocks: 'randomizeStocks',
          fetchData: 'loadData'
        }),
        endDay() {
          this.randomizeStocks();
        },
        handleDropdown() {
          this.openDropdown = !this.openDropdown
        },
        saveData() {
          const data = {
            funds: this.$store.getters.funds,
            stockPortfolio: this.$store.getters.stockPortfolio,
            stocks: this.$store.getters.stocks
          };
          this.$http.put('data.json', data);
        },
        loadData() {
          this.fetchData();
        }
      },
      created() {
        this.fetchData();
      }
    }
</script>

<style scoped>
  .active {
    font-color: black;
  }
  .navbar {
    border: 1px solid rgba(201, 201, 201, .3);
  }
  #end {
    cursor: pointer;
  }
  a:hover {
    cursor: pointer;
  }
</style>
