<template>
  <div class="container"  id="summary">
    <h1><strong>Occupation Overview</strong></h1>
    <div v-if="loaded">
      <span>{{this.occupation}} in {{this.region}}</span>
      <div class="separator"/>

      <Summary :occupation="occupation" :summary="summary"/>
      <div class="separator"/>

      <RegionalTrends :trendComparison="trendComparison" />
      <div class="separator"/>

      <RelatedIndustries 
        :occupation="occupation" 
        :employingIndustries="employingIndustries"
      />
      </div>
      <div v-else class="d-flex justify-content-center">
        <div class="spinner-border text-primary" role="status">
          <span class="sr-only"></span>
      </div>
    </div>
  </div>
</template>

<script>

import Summary from './OccupationComponents/Summary.vue'
import RelatedIndustries from './OccupationComponents/RelatedIndustries.vue'
import RegionalTrends from './OccupationComponents/RegionalTrends.vue'
import axios from 'axios';


export default {
  name: 'OccupationOverview',
  components: {
      Summary,
      RelatedIndustries,
      RegionalTrends
  },
  data: function () {
    return {
      loaded:false,
      occupation:null,
      region:null,
      summary:null,
      jobsGrowth:null,
      employingIndustries:null,
      trendComparison:null,
    }
  },
  mounted: function () {
    //Get data on component load
    this.getOccupationData();
  },
  methods: {
    getOccupationData() {

      axios.get('https://run.mocky.io/v3/a2cc3707-8691-4188-8413-6183a7bb3d32').then((response) => {
        //Set Component Data
        this.occupation = response.data.occupation.title;
        this.region = response.data.region.title;
        this.summary = response.data.summary;
        this.employingIndustries = response.data.employing_industries;
        this.trendComparison = response.data.trend_comparison;

        this.loaded=true;
      });
    }
  },


}
</script>
