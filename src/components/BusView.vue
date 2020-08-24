<template>
  <v-container>

    <v-row fluid>
      <v-col cols="12">
       <v-btn
          v-for="(stop, i) in stopNumbers"
          :key="i"
          class="mr-5"
          color="orange"
          @click="getStopData(stop)"
        >
        Stop {{stop}}
        </v-btn>

        <v-text-field
          
          class="mt-5"
          label="Enter stop number"
          v-model="manualSearch"
          :loading="loading"
        >
        </v-text-field>

        <v-btn
          class="mr-5"
          color="orange"
          @click="getStopData(manualSearch)"
        >
        Search {{manualSearch}}
        </v-btn>

      </v-col>
    </v-row>
  
     <v-row dense v-if="stopData">
        <v-col cols="12">
          <v-card
            color="red"
            dark
          >
            <v-card-title class="headline">Upcoming departures for stop {{stopData.Stop.Sms}} </v-card-title>
            <v-card-subtitle>{{stopData.Notices[0].LineNote}}</v-card-subtitle>
          </v-card>
        </v-col>

        <v-col
          v-for="(service, i) in stopData.Services"
          :key="i"
          cols="12"
        >
          <v-card
            color="blue"
            dark
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div>
                <v-card-title
                  class="headline"
                  v-text="new Date(service.DisplayDeparture).toString().split('GMT')[0]"
                ></v-card-title>

                <v-card-subtitle v-text="service.DestinationStopName"></v-card-subtitle>
              </div>

            </div>
          </v-card>
        </v-col>
      </v-row>

    
  </v-container>
</template>

<script>
export default {

  name: 'BusView',
  
  data:() => ({
    loading: false,
    stopData: null,
    stopNumbers: [4117,4118],
    manualSearch: 4117
  }),
  created(){
 

  },
  methods: {
    getStopData(stopNumber){
      this.loading = true
      fetch(`https://cors-anywhere.herokuapp.com/www.metlink.org.nz/api/v1/StopDepartures/${stopNumber}`)
      .then(response => response.json())
      .then(data => {
        console.log(data)
        this.stopData = data
        this.loading = false
      })
      .catch(err => console.log(err))
      }
  }
}
</script>

<style>

</style>