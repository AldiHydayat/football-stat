<template>
  <table @resize="checkSize($event)">
    <thead>
      <th>{{ isDesktop ? "Position" : "Pos" }}</th>
      <th>Club</th>
      <th>{{ isDesktop ? "Won" : "W" }}</th>
      <th>{{ isDesktop ? "Drawn" : "D" }}</th>
      <th>{{ isDesktop ? "Lost" : "L" }}</th>
      <th>{{ isDesktop ? "Played" : "P" }}</th>
      <th v-if="isDesktop">
        <abbr title="Goals For">GF</abbr>
      </th>
      <th v-if="isDesktop">
        <abbr title="Goals Against">GA</abbr>
      </th>
      <th>
        <abbr title="Goal Difference">GF</abbr>
      </th>
      <th>{{ isDesktop ? "Points" : "Pts" }}</th>
    </thead>
    <tbody>
      <tr :key="stat.team.id" v-for="stat in standing">
        <td>{{ stat.position }}</td>
        <td class="team-name">
          <img :src="stat.team.crestUrl" :alt="stat.team.name" />
          <span v-if="isDesktop">
            {{ stat.team.name }}
          </span>
        </td>
        <td>{{ stat.won }}</td>
        <td>{{ stat.draw }}</td>
        <td>{{ stat.lost }}</td>
        <td>{{ stat.playedGames }}</td>
        <td v-if="isDesktop">{{ stat.goalsFor }}</td>
        <td v-if="isDesktop">{{ stat.goalsAgainst }}</td>
        <td>{{ stat.goalDifference }}</td>
        <td>{{ stat.points }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "StandingTable",
  props: ["standing", "league"],
  data() {
    return {
      isDesktop: true,
    };
  },
  methods: {
    checkWindowSize() {
      let width = window.innerWidth;

      if (width <= 576) {
        this.isDesktop = false;
      } else {
        this.isDesktop = true;
      }
    },
  },
  created() {
    window.onload = this.checkWindowSize;
    window.onresize = this.checkWindowSize;
  },
};
</script>

<style lang="scss" scoped>
* {
  overflow-x: auto;
}
table {
  width: 100%;
  font-family: $reem;

  th,
  td {
    text-align: center;
  }

  .team-name {
    display: flex;
    align-items: center;
    img {
      width: 25px;
      height: auto;
      margin-right: 10px;
    }
  }

  td {
    padding: 10px;
  }
}
</style>
