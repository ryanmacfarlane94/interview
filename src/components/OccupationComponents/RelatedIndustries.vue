<template>
    <h2><strong>Industries Employing {{occupation}}</strong></h2>
    <div class="divider"></div>
    <div class="related-industries-container">
      <table>
        <tr>
          <th class="col-58">Industry</th>
          <th class="col-14">Occupation Jobs in Industry ({{employingIndustries.year}})</th>
          <th class="col-14">% of Occupation in Industry ({{employingIndustries.year}})</th>
          <th class="col-14">% of Total Jobs in Industry ({{employingIndustries.year}})</th>
        </tr>
        <tr v-for="item in employingIndustries.industries" v-bind:key="item.naics">
          <!--Set Css Variables for Percent-->
          <td class="col-58" :style="{
              '--percent':getOccupationPercent(item.in_occupation_jobs,totalJobs) + '%'
            }">
            <div class="bar"></div>
            <div class="text">{{ item.title }}</div>
          </td>
          <td class="col-14">{{ item.in_occupation_jobs }}</td>
          <td class="col-14">{{ getOccupationPercent(item.in_occupation_jobs,employingIndustries.jobs) }}%</td>
          <td class="col-14">{{ getOccupationPercent(item.in_occupation_jobs,item.jobs) }}%</td>
        </tr>
      </table>
    </div>
</template>

<script>

import '../../assets/styles/OccupationComponents/related_industries.css';

export default {
  name: 'RelatedIndustries',
  props: {
      occupation: String,
      employingIndustries: Object
  },
  data: function () {
    return {
      percent:0,
      totalJobs:0
    }
  },
  mounted: function () {
    for (var i = 0;i < this.employingIndustries.industries.length;i++) {
      this.totalJobs += this.employingIndustries.industries[i].in_occupation_jobs;
    }
  },
  methods: {
    getOccupationPercent(jobs, total_jobs) {
      var result = jobs / total_jobs * 100;
      return result.toFixed(1); 
    },
  }
}
</script>