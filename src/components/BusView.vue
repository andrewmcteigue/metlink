<template>
  <v-container>
    

    <v-row dense v-if="stopData">
        <v-col cols="12">
          <v-card
            color="red"
            dark
          >
            <v-card-title class="headline">Upcoming departures for stop 4118</v-card-title>
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
    stopData: null
  }),
  // filters: {
  //   formateDate(value){
  //     return "yo"
  //   }
  // },
  created(){
    fetch('https://cors-anywhere.herokuapp.com/www.metlink.org.nz/api/v1/StopDepartures/4118')
    .then(response => response.json())
    .then(data => {
      console.log(data)
      this.stopData = data
    })
    .catch(err => console.log(err))

  }
}
</script>

<style>

</style>