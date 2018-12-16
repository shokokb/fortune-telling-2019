<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <!--span>Vuetify</span-->
        <span class="font-weight-light">{{year}}年を占う</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>

    <v-content>
      <FortuneTelling :year='year' />
    </v-content>
  </v-app>
</template>

<script>
import FortuneTelling from './components/FortuneTelling'

export default {
  name: 'App',
  components: {
    FortuneTelling
  },
  data () {
    return {
      year : (new Date()).getFullYear() + ((new Date()).getMonth() > 6 ? 1 : 0),
    }
  },
}
</script>
