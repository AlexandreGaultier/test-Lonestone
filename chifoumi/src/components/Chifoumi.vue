<template>
  <v-container class="fill-height">
    <v-responsive class="align-centerfill-height mx-auto" max-width="900">

      <div class="text-center">

        <h1 class="text-h2 font-weight-bold">Chifoumi</h1>
        <p>Jouez un coup ! ;)</p>
      </div>

      <div class="py-4" />

      <v-row style="justify-content: center; align-items: center; gap: 20px;">
          <v-btn class="m-8 p-4" variant="outlined" color="grey"> <h1>Pierre</h1></v-btn>
        <v-card class="m-8 p-4">
          <h1>Feuille</h1>
        </v-card>
        <v-card class="m-8">
          <h1>Ciseaux</h1>
        </v-card>

      </v-row>
    </v-responsive>
  </v-container>
</template>

<script>
export default {
  name: 'Chifoumi',
  data( ) {    
    return {
      userChoice: "",
      botChoice: ""
    }
  }
}
</script>
