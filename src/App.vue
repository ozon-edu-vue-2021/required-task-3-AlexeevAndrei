<template>
  <div id="app">
    <div class="office">
      <Map :tables="tables" :legend="legend" @clickHandler="onClickHandler" />
      <SideMenu
        :person="person"
        :isUserOpenned="isUserOpenned"
        @closeProfile="onCloseProfile"
        :legend="legend"
        v-click-outside="hide"
      />
    </div>
  </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import tables from "@/assets/data/tables.json";
import legend from "@/assets/data/legend.json";
import people from "@/assets/data/people.json";
import ClickOutside from "vue-click-outside";

export default {
  name: "App",
  components: {
    Map,
    SideMenu,
  },

  directives: {
    ClickOutside,
  },

  data: () => ({
    tables: [],
    legend: [],
    people: [],
    person: {},
    isUserOpenned: false,
  }),

  created() {
    this.tables = tables;
    this.people = people;
    this.legend = this.getCounter(this.tables, legend);
  },

  methods: {
    getCounter(tables, legend) {
      let res = legend.map((legendItem) => {
        let counter = 0;
        tables.forEach((table) => {
          if (table.group_id === legendItem.group_id) {
            counter++;
          }
        });
        return {
          ...legendItem,
          counter,
        };
      });
      return res;
    },

    onClickHandler(id) {
      this.person = this.people.find((person) => person.tableId === id);
      this.isUserOpenned = true;
    },

    onCloseProfile() {
      this.isUserOpenned = false;
    },

    hide() {
      this.isUserOpenned = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

* {
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

.office {
  display: grid;
  grid-template-columns: 1fr 320px;
  border-radius: 6px;
  border: 1px solid #ccd8e4;
  height: 100%;
  background: white;
  max-width: 1500px;
  margin: 0 auto;
}
</style>
