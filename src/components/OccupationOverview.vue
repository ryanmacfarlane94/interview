<template>
  <div class="container"  id="summary">
    <h1><strong>Occupation Overview</strong></h1>
    <span>{{this.occupation}} in {{this.region}}</span>
    <div class="separator"/>
    
    <Summary v-if="loaded" :occupation="occupation" :summary="summary"/>
    <div class="separator"/>
    
    <RegionalTrends v-if="loaded" :trendComparison="trendComparison" />
    <div class="separator"/>

    <RelatedIndustries 
      v-if="loaded" 
      :occupation="occupation" 
      :employingIndustries="employingIndustries"
    />
  </div>
</template>

<script>
import Summary from './OccupationComponents/Summary.vue'
import RelatedIndustries from './OccupationComponents/RelatedIndustries.vue'
import RegionalTrends from './OccupationComponents/RegionalTrends.vue'

//import axios from 'axios';


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
      trendComparison:null
    }
  },
  mounted: function () {
    //Get data on component load
    this.getOccupationData();
  },
  methods: {
    getOccupationData() {
        var response = {};
        response.data = {
  occupation: {
    onet: "15-1131",
    title: "Computer Programmers"
  },
  region: {
    type: "MSA",
    id: "42660",
    title: "Seattle-Tacoma-Bellevue, WA"
  },
  summary: {
    jobs: {
      year: 2015,
      regional: 12352,
      national_avg: 6501
    },
    jobs_growth: {
      start_year: 2013,
      end_year: 2018,
      regional: 10.2,
      national_avg: 8.5
    },
    earnings: {
      regional: 57.24,
      national_avg: 38.2
    }
  },
  trend_comparison: {
    start_year: 2013,
    end_year: 2018,
    regional: [
      11904,
      12384,
      12352,
      12680,
      12920,
      13114
    ],
    state: [
      13103,
      13598,
      13599,
      13968,
      14244,
      14469
    ],
    nation: [
      300651,
      307024,
      314154,
      318998,
      326205
    ]
  },
  employing_industries: {
    year: 2015,
    jobs: 12352,
    industries: [
      {
        naics: "511210",
        title: "Software Publishers",
        in_occupation_jobs: 4654,
        jobs: 52886
      },
      {
        naics: "541512",
        title: "Computer Systems Design Services",
        in_occupation_jobs: 1873,
        jobs: 20582
      },
      {
        naics: "541512",
        title: "Custom Computer Programming Services",
        in_occupation_jobs: 1388,
        jobs: 15252
      },
      {
        naics: "541512",
        title: "Aircraft Manufacturing",
        in_occupation_jobs: 444,
        jobs: 71612
      },
      {
        naics: "541512",
        title: "Other Computer Related Services",
        in_occupation_jobs: 296,
        jobs: 3245
      }
    ]
  }
};
        this.occupation = response.data.occupation.title;
        this.region = response.data.region.title;
        this.summary = response.data.summary;
        this.employingIndustries = response.data.employing_industries;
        this.trendComparison = response.data.trend_comparison;

        this.loaded=true;

      /*axios.get('https://run.mocky.io/v3/a2cc3707-8691-4188-8413-6183a7bb3d32').then((response) => {
        //console.log(response.data);
        //Set Component Data

      });*/
    }
  },


}
</script>
