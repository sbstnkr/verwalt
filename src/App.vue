<template>
  <v-app>
    <v-overlay :value="isOverlaid">
    </v-overlay>
    <v-app-bar
      app
      dark
      clipped-left
      id="app-bar"
    >
      <v-spacer></v-spacer>
      <v-app-bar-title class="text-center text-h6 ml-3">V E R W A L T</v-app-bar-title>
      <v-spacer></v-spacer>
      <v-menu
      transition="slide-y-transition"
      bottom
      nudge-bottom=56
      >
      <template v-slot:activator="{ on, attrs }">
      <v-btn icon class="mr-3" v-bind="attrs"
          v-on="on">
        <v-hover 
        v-slot="{ hover }"
        open-delay="100">
        <v-avatar
          :class="hover ? 'elevation-8' : 'elevation-3'"
          size="42">
          <v-img
            :src="image"
            :key="image"
          ></v-img>
        </v-avatar>
      </v-hover>
      </v-btn>
      </template>
      <v-list rounded dark color="#404040">
        <v-list-item
          v-for="(item, i) in menu_options"
          :key="i"
          link
        >
          <v-list-item-title class="text-right">{{ item }}</v-list-item-title>
          <v-list-item-title class="text-right" v-if="item='Account settings'" @click="isOverlaid = true">{{ item }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    </v-app-bar>
    <v-navigation-drawer clipped app absolute permanent>
      <v-list>
          <v-list-item
            @click="fieldClicked(field.title)"
            v-for="field in fields"
            :key="field.title"
            link
          >
            <v-list-item-icon class="ml-3">
              <v-icon>{{ field.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title class="font-weight-medium">{{ field.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>
    <v-main>
      <v-container fluid>
        <v-card flat v-if=isSubscriptionsClicked>
          <v-card-title class="text-h4 font-weight-bold">My subscriptions</v-card-title>
          <v-divider></v-divider>
          <v-card flat class="d-flex flex-column">
            <v-card flat class="mb-5">
          <v-card flat class="d-flex flex-row">
          <v-card-subtitle class="text-h5 d-inline-flex align-center font-weight-medium">Electricity
            <v-img :src="electricity.icon" height=50 width=50 contain class="ml-5"></v-img>
          </v-card-subtitle>
          </v-card>
          <v-card-text class="ml-5 text-body-1">Provider:</v-card-text>
            <v-template class="mt-5 d-flex flex-row justify-center">
            <v-icon small v-for="n in 3" :key="n">mdi-lightning-bolt</v-icon>
            </v-template>
          </v-card >
          
          
          <v-card flat class="d-flex flex-row">
          <v-card-subtitle class="text-h5 d-inline-flex align-center font-weight-medium">Cable
            <v-img :src="cable.icon" height=70 width=70 contain class="ml-5"></v-img>
          </v-card-subtitle>
          </v-card>
          <v-card-text class="ml-5 text-body-1">Provider:</v-card-text>
            <v-template class="mt-5 d-flex flex-row justify-center">
            <v-icon small v-for="n in 3" :key="n">mdi-television-box</v-icon>
            </v-template>
          </v-card>
        </v-card>
        <v-card flat v-if=isPaymentsClicked>
          <v-card-title class="text-h4">My Payments</v-card-title>
        </v-card>
        <v-card flat v-if=isNewsClicked>
          <v-card-title class="text-h4">News</v-card-title>
        </v-card>

      </v-container>
    </v-main>
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  //components: {
  //  HelloWorld,
  //},

  data: () => ({
    image: require('@/assets/avatars/seba.jpg'),
    menu_options: ['Account settings', 'Sign out'],
    fields: [
      { title: 'Payments', icon: 'mdi-credit-card-outline' },
      { title: 'News', icon: 'mdi-newspaper-variant-multiple' },
      { title: 'Subscriptions', icon: 'mdi-playlist-check' }
    ],
    electricity: { name: 'Tauron', icon: require('@/assets/subscriptions/tauron.jpg') },
    cable: { name: 'Netia', icon: require('@/assets/subscriptions/netia.jpeg') },
    isPaymentsClicked: true,
    isNewsClicked: false,
    isSubscriptionsClicked: false,
    isOverlaid: false
  }),
  methods: {
    fieldClicked(field_title) {
      switch (field_title) {
        case 'Payments': 
          this.isPaymentsClicked = true;
          this.isNewsClicked = false;
          this.isSubscriptionsClicked = false;
          break;
        case 'News': 
          this.isNewsClicked = true; 
          this.isPaymentsClicked = false;
          this.isSubscriptionsClicked = false;
          break;
        case 'Subscriptions': 
          this.isSubscriptionsClicked = true;
          this.isPaymentsClicked = false;
          this.isNewsClicked = false;
      }
    }
  }
};
</script>
<style scoped>
  #app-bar {
    background: linear-gradient(90deg, #616161 0%, #212121 0%, #424242 100%);
    }
</style>
