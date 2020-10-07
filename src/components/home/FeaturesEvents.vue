<template>
  <v-container fluid class="mb-1">
    <v-row align="center" justify="center" class>
      <v-col cols="12" md="12" lg="12" sm="12" class="mb-0">
        <p
          class="google-font mb-0 mt-0"
          style="font-weight: 350;font-size:180%"
        >
          <b>
            Our
            <span style="color: #1a73e8;">Events</span>
            &
            <span style="color: #1a73e8;">Meetups</span>
          </b>
        </p>
        <p class="google-font mt-0 mb-0" style="font-size:95%">
          Our Upcomming Events.
        </p>
      </v-col>
      <v-col cols="12" md="12" lg="12" sm="12" class="mt-0 pt-0 pa-0">
        <v-container fluid class="py-0 my-0">
          <v-row class="py-0 my-0" v-if="loading">
            <v-col
              v-for="i in 4"
              :key="i"
              md="3"
              lg="3"
              sm="6"
              cols="6"
              class="pa-2"
            >
              <v-sheet
                :color="`grey ${theme.isDark ? 'darken-2' : 'lighten-4'}`"
                class
              >
                <v-skeleton-loader
                  class="mx-auto"
                  type="article"
                ></v-skeleton-loader>
              </v-sheet>
            </v-col>
          </v-row>

          <v-row class="py-0 my-0 px-2">
            <v-col
              v-for="(item, i) in featureEvendsData"
              :key="i"
              md="3"
              lg="3"
              sm="6"
              cols="6"
              class="pa-1"
            >
             
              <featureEventCard :data="item" />
            </v-col>
          </v-row>
        </v-container>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import service from "@/services/appservices";
import axios from "axios";

export default {
  name: "App",
  inject: ["theme"],
  components: {
    featureEventCard: () => import("@/components/home/FeatureEventCard"),
  },
  data: () => ({
    loading: false,

    FeaturesEventID: [],
    AllCustomEvents: [],
    eData: [],
    featureEvendsData: [
      
    ],
  }),
  created() {
    let self = this;

    var config = {
      method: "get",
      url:
        "https://cors-anywhere.herokuapp.com/https://api.meetup.com/gdg-settat/events?&photo-host=public&page=20",
      headers: {
        origin: "x-requested-with",
      },
    };

    axios(config)
      .then(function(response) {
        response.data.forEach((element) => {
          self.featureEvendsData.push(element);
        });

        //console.log(self.featureEvendsData)
      })
      .catch(function(error) {
        console.log(error);
      });
  },
};
</script>

<style scoped>
.lightModeCardFeatureEvent {
  background-color: #ffff;
  box-shadow: 0 0 36px rgba(0, 0, 0, 0.1);

  border-radius: 8px;
}
.darkModeCardFeatureEvent {
  background-color: #292929;
  box-shadow: 0 0 36px rgba(0, 0, 0, 0.1);
  /* border:1px solid #212121; */
  border: 1px solid #424242;
  border-radius: 8px;
}
</style>
