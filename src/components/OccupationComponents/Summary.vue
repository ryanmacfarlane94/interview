<template>
    <h2><strong>Occupation Summary for {{occupation}}</strong></h2>
    <div class="container">
      <div class="row summary-border">
        <div class="col-md center">
            <span class="summary-stat">{{summary.jobs.regional}}</span><br>
            <span class="summary-label">Jobs ({{summary.jobs.year}})</span><br>
            <span class="summary-description">{{compareToNationalAvg()}}% <span id="jobs-avg">{{compareToNationalAvgText()}}</span> National Average</span>
        </div>
        <div class="col-md center summary-border-left">
            <span class="summary-stat" id="jobs-growth-regional">{{getGrowthSign(summary.jobs_growth.regional)}}{{summary.jobs_growth.regional}}%</span><br>
            <span class="summary-label">% Change ({{summary.jobs_growth.start_year}}-{{summary.jobs_growth.end_year}})</span><br>
            <span class="summary-description">Nation: <span id="jobs-growth-national">{{getGrowthSign(summary.jobs_growth.national_avg)}}{{summary.jobs_growth.national_avg}}%</span></span>
        </div>
        <div class="col-md center summary-border-left">
            <span class="summary-stat">${{summary.earnings.regional}}/hr</span><br>
            <span class="summary-label">Median Hourly Earnings</span><br>
            <span class="summary-description">Nation: ${{summary.earnings.national_avg.toFixed(2)}}/hr</span>
        </div>
      </div>
    </div>
</template>

<script>

import '../../assets/styles/OccupationComponents/summary.css';

export default {
  name: 'Summary',
  props: {
    occupation: String,
    summary: Object,
    jobsGrowth: Object
  },
  mounted: function () {
    //Set Colors for valuse > or < 0
    this.setColor(this.compareToNationalAvg() - 100, 'jobs-avg');
    this.setColor(this.summary.jobs_growth.regional, 'jobs-growth-regional');
    this.setColor(this.summary.jobs_growth.national_avg, 'jobs-growth-national');
  },
  methods: {
    //Helper Functions
    compareToNationalAvg() {
      return parseInt(this.summary.jobs.regional / this.summary.jobs.national_avg * 100);
    },

    compareToNationalAvgText() {
      var percent = this.summary.jobs.regional / this.summary.jobs.national_avg;
      if (percent > 1) {
        return "above";
      }
      else if (percent < 1) {
        return "below";
      } 
      else {
        return "(same as)";
      }
    },

    getGrowthSign(input) {
      if (input >= 0) {
        return '+';
      }
      return "";
    },

    setColor(value,elementId) {
      var element = document.getElementById(elementId);
      element.classList.remove('green');
      element.classList.remove('red');
      if (value > 0) {
        element.classList.add('green');
      }
      if (value < 0) {
        element.classList.add('red');
      }
    }
  }
}
</script>
