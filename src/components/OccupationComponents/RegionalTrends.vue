<template>
    <h2><strong>Regional Trends</strong></h2>
    <div class="divider"></div>
    <div id="chart" class="chart"></div>
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
            <td class="col-md-8"><img src="/img/circle.JPG" class="point"/>&emsp;Region</td>
            <td class="col-md">{{ trendComparison.regional[0].toLocaleString() }}</td>
            <td class="col-md">{{ trendComparison.regional[trendComparison.regional.length - 1].toLocaleString() }}</td>
            <td class="col-md">{{ (trendComparison.regional[trendComparison.regional.length - 1] - trendComparison.regional[0]).toLocaleString() }}</td>
            <td class="col-md">{{ getChange(trendComparison.regional) }}%</td>
        </tr>
        <tr>
            <td class="col-md-8"><img src="/img/square.JPG" class="point"/>&emsp;State</td>
            <td class="col-md">{{ trendComparison.state[0].toLocaleString() }}</td>
            <td class="col-md">{{ trendComparison.state[trendComparison.state.length - 1].toLocaleString() }}</td>
            <td class="col-md">{{ (trendComparison.state[trendComparison.state.length - 1] - trendComparison.state[0]).toLocaleString() }}</td>
            <td class="col-md">{{ getChange(trendComparison.state) }}%</td>
        </tr>
        <tr>
            <td class="col-md-8"><img src="/img/triangle.JPG" class="point"/>&emsp;Nation</td>
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
import {GoogleCharts} from 'google-charts';


export default {
  name: 'RegionalTrends',
  props: {
      trendComparison: Object
  },
  mounted: function () {
    GoogleCharts.load(this.drawChart);
  },
  methods: {
    getChange(data) {
        var change = data[data.length - 1] - data[0];
        return (change / data[0] * 100).toFixed(1).toLocaleString();
    },
    drawChart() {
        const data = GoogleCharts.api.visualization.arrayToDataTable(this.getData());
        const chart = new GoogleCharts.api.visualization.LineChart(document.getElementById('chart'));
        var options = {
          legend: { position: 'bottom' },
          vAxis: {
            title: 'Percentage Change'
          },
          pointSize: 5,
          series: {
            0: { color: '#001145', pointShape: 'circle' },
            1: { color: '#14ACDE', pointShape: 'square'},
            2: { color: '#95E5FF', pointShape: 'triangle' }
          }
        };

        chart.draw(data, options);
    },
    getData() {
        var data = [
            ['Year','Region','State','Nation'],
            [this.trendComparison.start_year.toString(),0,0,0]
        ];
        var i;
        var year = this.trendComparison.start_year + 1;
        for (i = 1;i < this.trendComparison.regional.length;i++) {
            var regionChange = (this.trendComparison.regional[i] - this.trendComparison.regional[0]) / this.trendComparison.regional[0] * 100;
            var stateChange = (this.trendComparison.state[i] - this.trendComparison.state[0]) / this.trendComparison.state[0] * 100;
            var nationChange = (this.trendComparison.nation[i] - this.trendComparison.nation[0]) / this.trendComparison.nation[0] * 100;
            data.push([year.toString(), regionChange, stateChange, nationChange]);
            year++;
        }
        return data;
    }
  }
}
</script>