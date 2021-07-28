<template>
  <div id="detail-and-controls-cnt">
    <div id="detail-component-cnt">
      <div
        class="detail-component"
        v-if="Object.keys(selectedPlayer).length === 0"
      >
        <h3 id="detail-cover">Please select a Card.</h3>
      </div>
      <div v-else class="detail-component">
        <DetailView :player="selectedPlayer"></DetailView>
      </div>
    </div>
    <div id="controls-cnt">
      <h1>Controls</h1>
      <div id="controls-btn-cnt">
        <div>
          <button class="btn1" @click="sortAsc">Sort Asc</button>
        </div>
        <div>
          <button class="btn1" @click="sortDesc">Sort Desc</button>
        </div>
        <div>
          <form v-on:submit.prevent="submitCard">
            <button class="btn1">Submit</button>
          </form>
        </div>
      </div>
    </div>
  </div>
  <div id="overview-outer-cnt">
    <div id="overview-inner-cnt">
      <h1>Overview</h1>
      <div id="select-button-cnt">
        <button
          v-for="player in players"
          :key="player.realName"
          :class="['select-button', { active: selectedPlayer === player }]"
          @click="selectedPlayer = player"
        >
          <p>- {{ player.realName }}</p>
          <p>- {{ player.playerName }}</p>
          <p>- {{ player.asset }}</p>
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import DetailView from "./components/DetailView.vue";
import axios from "axios";
import json from "./assets/Data.json";
import PlayerInterface from "./interfaces/PlayerInterface.vue";
import PlayerClass from "./classes/Player.vue";

export default defineComponent({
  name: "App",
  components: {
    DetailView,
  },
  // async setup() {   // use this for api call
  //   try {
  //     const result = await axios.get(
  //       'someUrl'
  //     );
  //     const players:any[] = [];
  //     for (const player of result) {
  //       let newPlayer = Object.assign(new PlayerClass(), player);
  //       players.push(newPlayer)
  //     }
  //     return { players };
  //   } catch (error) {
  //     console.log(error);
  //   }
  // },
  data() {
    return {
      players: json, // data for development
      selectedPlayer: {},
    };
  },
  computed: {
    getCurrentPlayer(): any {
      return this.selectedPlayer;
    },
    getsSortedPlayers(): any {
      return this.players;
    },
  },
  methods: {
    sortAsc() {
      this.players = this.players.sort((a: any, b: any) =>
        a.realName > b.realName ? 1 : -1
      );
    },
    sortDesc() {
      this.players = this.players.sort((a: any, b: any) =>
        a.realName > b.realName ? -1 : 1
      );
    },
    // submitCard() {   // post to backend
    //   axios.post('someUrl', this.selectedPlayer)
    //     .then((result) => {
    //       // success
    //     }).catch((error) => {
    //       // handle error
    //     }).finally(() => {
    //       // some action
    //     });
    // }
  },
});
</script>

<style>
body {
  background-image: radial-gradient(
    circle at 10% 20%,
    rgb(255, 209, 67) 0%,
    rgb(231, 95, 16) 90%
  );
  background-size: 100% 100%;
  background-repeat: no-repeat;
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
}
#detail-and-controls-cnt {
  display: flex;
  margin-left: 25px;
}
#detail-component-cnt {
  height: 385px;
  width: 650px;
  background-color: rgba(0, 0, 0, 0.2);
  border-radius: 50px;
}
.detail-component {
  margin-left: 25px;
}
#controls-cnt {
  width: 250px;
  text-align: center;
  border-radius: 50px;
  background-color: rgba(0, 0, 0, 0.2);
  margin-left: 25px;
}
#controls-btn-cnt {
  width: 100%;
}
#controls-btn-cnt div {
  display: flex;
  justify-content: center;
  align-items: center;
}
.btn1 {
  width: 160px;
  font-size: 16px;
  font-weight: 600;
  color: #fff;
  cursor: pointer;
  margin: 20px;
  height: 55px;
  text-align: center;
  border: none;
  background-size: 300% 100%;
  border-radius: 50px;
  -o-transition: all 0.4s ease-in-out;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
  background-image: linear-gradient(to right, #f5ce62, #e43603, #e85a19);
  box-shadow: 0 4px 15px 0 #b15f43bf;
}
.btn1:hover {
  background-position: 100% 0;
  -o-transition: all 0.4s ease-in-out;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
}
.btn1:focus {
  outline: none;
}
#detail-cover {
  text-align: center;
}
#overview-outer-cnt {
  display: flex;
  margin-left: 25px;
  border-radius: 50px;
  background-color: rgba(0, 0, 0, 0.2);
  color: #fff;
  width: 925px;
  height: 450px;
  margin-top: 25px;
}
#overview-inner-cnt {
  margin-left: 25px;
}
#select-button-cnt {
  display: flex;
  flex-wrap: wrap;
  width: 905px;
}
.select-button {
  list-style: none;
  flex: 1 0 25%;
  min-width: 0;
  padding: 6px 10px;
  margin-right: 30px;
  margin-bottom: 30px;
  font-weight: 600;
  color: #fff;
  cursor: pointer;
  text-align: center;
  border: none;
  background-size: 300% 100%;
  border-radius: 50px;
  -o-transition: all 0.4s ease-in-out;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
  background-image: linear-gradient(to right, #f5ce62, #e43603, #e85a19);
  box-shadow: 0 4px 15px 0 #b15f43bf;
}
.select-button:hover {
  background-position: 100% 0;
  -o-transition: all 0.4s ease-in-out;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
}
.select-button p {
  font-size: large;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
.select-button.active {
  background-position: 25% 100%;
  -o-transition: all 0.4s ease-in-out;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-ou;
}
</style>
