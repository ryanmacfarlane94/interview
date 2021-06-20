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
          <td>Test</td>
          <td>{{ item.in_occupation_jobs }}</td>
          <td></td>
          <td></td>
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
  mounted: function () {

  },
  methods: {
    getOccupationPercent(jobs, total_jobs) {
      var result = jobs / total_jobs;
      return result.toFixed(2); 
    }
  }
}
</script>
