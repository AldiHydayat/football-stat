<template>
  <section id="standings">
    <div class="container">
      <div class="league-list">
        <ul>
          <li>
            <a
              href="#standings"
              :class="[currentLeagueCode === 'PL' ? 'active' : '']"
              @click="changeLeague('PL')"
            >
              <img
                src="https://a.espncdn.com/i/leaguelogos/soccer/500/23.png"
                alt="EPL"
              />
            </a>
          </li>
          <li>
            <a
              href="#standings"
              :class="[currentLeagueCode === 'PD' ? 'active' : '']"
              @click="changeLeague('PD')"
              ><img
                src="https://a.espncdn.com/i/leaguelogos/soccer/500/15.png"
                alt="La Liga"
            /></a>
          </li>
          <li>
            <a
              href="#standings"
              :class="[currentLeagueCode === 'SA' ? 'active' : '']"
              @click="changeLeague('SA')"
              ><img
                src="https://a.espncdn.com/i/leaguelogos/soccer/500/12.png"
                alt="Serie A"
            /></a>
          </li>
          <li>
            <a
              href="#standings"
              :class="[currentLeagueCode === 'FL1' ? 'active' : '']"
              @click="changeLeague('FL1')"
              ><img
                src="https://a.espncdn.com/i/leaguelogos/soccer/500/9.png"
                alt="Ligue 1"
            /></a>
          </li>
          <li>
            <a
              href="#standings"
              :class="[currentLeagueCode === 'BL1' ? 'active' : '']"
              @click="changeLeague('BL1')"
              ><img
                src="https://a.espncdn.com/i/leaguelogos/soccer/500/10.png"
                alt="Bundesliga"
            /></a>
          </li>
        </ul>
      </div>
      <div class="standing">
        <span id="loading" v-if="isLoading">
          <div class="loader"></div>
        </span>
        <standing-table :standing="standing" :league="currentLeague" />
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
import StandingTable from "../components/StandingTable.vue";

export default {
  name: "Standings",
  components: { StandingTable },
  data() {
    return {
      league: [],
      standing: [],
      currentLeague: "",
      currentLeagueCode: "PL",
      isLoading: false,
    };
  },
  async created() {
    this.isLoading = true;
    await axios
      .get(
        `http://api.football-data.org/v2/competitions/${this.currentLeagueCode}/standings`,
        {
          headers: { "X-Auth-Token": "b48408aabc3d46d2b0fc90e61f2d6dd8" },
        }
      )
      .then(async (res) => {
        this.currentLeague = res.data.competition.name;
        this.standing = res.data.standings[0].table;
        this.currentLeagueCode = res.data.competition.code;
      })
      .finally(() => {
        this.isLoading = false;
      });
  },
  methods: {
    async changeLeague(id) {
      this.isLoading = true;
      await axios
        .get(`http://api.football-data.org/v2/competitions/${id}/standings`, {
          headers: { "X-Auth-Token": "b48408aabc3d46d2b0fc90e61f2d6dd8" },
        })
        .then(async (res) => {
          this.currentLeague = res.data.competition.name;
          this.standing = res.data.standings[0].table;
          this.currentLeagueCode = res.data.competition.code;
        })
        .finally(() => {
          this.isLoading = false;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
section {
  background-color: #bbeef5;
  padding-top: 100px;
  box-sizing: border-box;
  min-height: 100vh;

  .container {
    .league-list {
      ul {
        display: flex;
        list-style-type: none;
        justify-content: space-evenly;

        .active {
          border-bottom: 2px solid #069200;
        }

        a {
          text-decoration: none;
          font-size: 18px;
          font-family: $reem;
          color: #069200;

          img {
            width: 50px;
            height: auto;
          }
        }
      }
    }

    .standing {
      position: relative;
      padding-top: 15px;

      #loading {
        background-color: rgba($color: #c4c4c4, $alpha: 0.5);
        display: flex;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        justify-content: center;

        .loader {
          margin-top: 50px;
          border: 10px solid #f3f3f3;
          border-top: 10px solid #3498db;
          border-radius: 50%;
          width: 50px;
          height: 50px;
          animation: spin 2s linear infinite;
        }

        @keyframes spin {
          0% {
            transform: rotate(0deg);
          }
          100% {
            transform: rotate(360deg);
          }
        }
      }
    }
  }
}
</style>
