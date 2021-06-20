<template>
    <h2><strong>Regional Trends</strong></h2>
    <div class="divider"></div>
    <div class="regional-trends-container">
      <table>
        <tr>
            <th class="col-md-8">Region</th>
            <th class="col-md">{{trendComparison.start_year}} jobs</th>
            <th class="col-md">{{trendComparison.end_year}} jobs</th>
            <th class="col-md">Change</th>
            <th class="col-md">% Change</th>
        </tr>
        <tr>
            <td class="col-md-8">Region</td>
            <td class="col-md">{{ trendComparison.regional[0].toLocaleString() }}</td>
            <td class="col-md">{{ trendComparison.regional[trendComparison.regional.length - 1].toLocaleString() }}</td>
            <td class="col-md">{{ (trendComparison.regional[trendComparison.regional.length - 1] - trendComparison.regional[0]).toLocaleString() }}</td>
            <td class="col-md">{{ getChange(trendComparison.regional) }}%</td>
        </tr>
        <tr>
            <td class="col-md-8">State</td>
            <td class="col-md">{{ trendComparison.state[0].toLocaleString() }}</td>
            <td class="col-md">{{ trendComparison.state[trendComparison.state.length - 1].toLocaleString() }}</td>
            <td class="col-md">{{ (trendComparison.state[trendComparison.state.length - 1] - trendComparison.state[0]).toLocaleString() }}</td>
            <td class="col-md">{{ getChange(trendComparison.state) }}%</td>
        </tr>
        <tr>
            <td class="col-md-8">Nation</td>
            <td class="col-md">{{ trendComparison.nation[0].toLocaleString() }}</td>
            <td class="col-md">{{ trendComparison.nation[trendComparison.nation.length - 1].toLocaleString() }}</td>
            <td class="col-md">{{ (trendComparison.nation[trendComparison.nation.length - 1] - trendComparison.nation[0]).toLocaleString() }}</td>
            <td class="col-md">{{ getChange(trendComparison.nation) }}%</td>
        </tr>
      </table>
    </div>
</template>

<script>

import '../../assets/styles/OccupationComponents/regional-trends.css';

export default {
  name: 'RegionalTrends',
  props: {
      trendComparison: Object
  },
  data: function () {
    return {

    }
  },
  mounted: function () {

  },
  methods: {
      getPercentChange() {

      },
      getChange(data) {
          var change = data[data.length - 1] - data[0];
          return (change / data[0] * 100).toFixed(1).toLocaleString();
      }
  }
}
</script>