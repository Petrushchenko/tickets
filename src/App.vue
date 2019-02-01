<template>
  <div id="app">
    <app-logo></app-logo>
    <div class="container">
      <app-filters @select="filterTickets"
                   @onChangeCurrency = "refreshPrice"
      >
        
      </app-filters>

      <ul>
        <app-ticket v-for="(ticket, i) in selectedTickets"
                    v-bind:ticket="ticket"
                    v-bind:key="i"
                    v-bind:factor = "factor"
                    v-bind:sign = "currencySign"

        >
        </app-ticket>
      </ul>
            
    </div>
  </div>
</template>

<script>

  import AppLogo from './components/Logo.vue';
  import AppFilters from './components/Filters.vue';
  import AppTicket from './components/Ticket.vue';
  import Data from './tickets.json';

export default {
  data() {
   return {
     tickets: Data.tickets,
     factor: 1,
     currencySign: "₱",
     filters: []
   }
  },
  components: {
    AppLogo: AppLogo,
    AppFilters: AppFilters,
    AppTicket: AppTicket
  },
  computed: {
    selectedTickets(){
      if (this.filters.length === 0 ) {
        return this.tickets;
      } else {
        return this.tickets.filter(ticket => this.filters.some(filter => filter == ticket.stops));
      }
    }
  },
  methods: {
    filterTickets(val) {

        if (val == "all") {
          this.filters = [];
        } else {
          this.filters.push(val);

        }
    },
    refreshPrice(str) {
      switch (str) {
        case 'usd':
          this.factor = 100;
          this.currencySign = "$";
          break;
        case 'eur':
          this.factor = 150;
          this.currencySign = "€";
          break;
        default:
          this.factor = 1;
          this.currencySign = "₱"
      }
    }
  }
}

</script>

<style lang="scss">
body {
  margin: 0;
  * {
    box-sizing: border-box;
  }

}
#app {
  font-family: OpenSans, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #F3F7FA;
  width: 1024px;
  margin: 0 auto;
  padding: 50px 100px 100px;
  .container {
    display: grid;
    grid-template-columns: 29% 70%;
    grid-column-gap: 1%;
    ul {
      margin: 0;
      padding: 0;
      list-style-type: none;
    }
  }
}
  
</style>
