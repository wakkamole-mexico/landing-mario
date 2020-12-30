<template>
  <v-app class="cursor">
    <transition name="fade">
      <div class="loading" v-if="loading">
        <div class="loading-text">
          <div style="width: 200px; height: 200px; margin: auto">
            <v-img max-width="200px" src="/img/loading.gif"></v-img>
          </div>
          <span class="loading-text-words">L</span>
          <span class="loading-text-words">O</span>
          <span class="loading-text-words">A</span>
          <span class="loading-text-words">D</span>
          <span class="loading-text-words">I</span>
          <span class="loading-text-words">N</span>
          <span class="loading-text-words">G</span>
        </div>
      </div>
    </transition>
    <template v-if="estatus">
      <v-app-bar app flat class="white">
        <v-img @click="$router.push({name: 'Home'})" style="max-width: 150px" src="/img/lego-mario.png"></v-img>
        <v-spacer />
        <v-img style="max-width: 200px" src="/img/juguetron.png"></v-img>
      </v-app-bar>
      <v-content>
        <v-container fluid class="ma-0 pa-0">
          <v-container
            class="pa-0 ma-0 fondo-mario"
            fluid
            style="height: calc(100vh - 65px)"
          >
            <v-card class="transparent">
              <v-card-text class="pa-0">
                <v-list-item class="pa-0">
                  <v-img
                    src="/img/gif5.gif"
                    max-width="240px"
                    style="height: calc(100vh - 65px)"
                    class="hidden-sm-and-down"
                  ></v-img>
                  <v-list-item-content class="pa-6">
                    <v-row>
                      <v-col cols="12">
                        <div
                          class="mb-2 white--text font-blink text-center"
                          :class="
                            $vuetify.breakpoint.mdAndUp
                              ? 'display-2'
                              : 'display-1'
                          "
                        >
                          ¡Lo lograste! Ya eres parte del Ejército Mario.
                        </div>
                        <div
                          class="mb-2 white--text font-blink text-center"
                          :class="
                            $vuetify.breakpoint.mdAndUp
                              ? 'display-1'
                              : 'headline'
                          "
                        >
                          Pronto recibirás noticias que te harán brincar de la
                          emoción.
                        </div>
                      </v-col>
                    </v-row>
                    <v-card class="transparent">
                      <v-card-text>
                        <v-row>
                          <v-col cols="12" class="text-center">
                            <img
                              :width="
                                $vuetify.breakpoint.mdAndUp ? '50%' : '100%'
                              "
                              :src="imagen"
                            />
                          </v-col>
                          <v-col cols="12" class="text-center" :class="$vuetify.breakpoint.smAndDown?'mb-12':''">
                            <template v-if="clave!=null">
                              <v-btn
                                      @click="facebook()"
                                      class="mx-4"
                                      color="primary"
                                      fab
                                      dark
                              >
                                <v-icon>mdi-facebook</v-icon>
                              </v-btn>
                              <v-btn
                                      class="mx-4"
                                      color="green"
                                      fab
                                      :href="'whatsapp://send?text=Únete al ejercito de Mario y ayúdalo: https://mario.juguetronmexico.mx/user.php?u='+this.clave"
                                      target="_blank"
                                      dark
                              >
                                <v-icon>mdi-whatsapp</v-icon>
                              </v-btn>
                              <v-btn class="mx-4" fab dark @click="descargar()">
                                <v-icon>mdi-download</v-icon>
                              </v-btn>
                            </template>
                            <v-btn @click="reset()" fab>
                              <v-icon>mdi-reload</v-icon>
                            </v-btn>
                          </v-col>
                        </v-row>
                      </v-card-text>
                    </v-card>
                  </v-list-item-content>
                </v-list-item>
              </v-card-text>
            </v-card>
            <v-img
              src="/img/gif5h.gif"
              width="100%"
              class="hidden-md-and-up"
              style="position: fixed; bottom: 0px;"
            ></v-img>
          </v-container>
        </v-container>
      </v-content>
    </template>
    <v-footer
            color="#000"
            padless
    >
      <v-row
              justify="center"
              no-gutters
      >
        <v-col
                style="background-color: #000"
                class="py-4 pl-4 text-left white--text"
                cols="12" md="6"
        >
          {{ new Date().getFullYear() }} <strong>Juguetron. All Rights Reserved.</strong>
        </v-col>
        <v-col cols="12" md="6" class="text-right">
          <v-btn
                  color="white"
                  text
                  rounded
                  class="my-2"
                  :to="{name: 'Privacidad'}"
          >
            Aviso de Privacidad
          </v-btn>
        </v-col>
      </v-row>
    </v-footer>
  </v-app>
</template>

<script>
import Vue from "vue";
import {mapGetters} from 'vuex';

export default Vue.extend({
  name: "Thanks",
  data: () => ({
    estatus: false,
    loading: true,
  }),
  mounted() {
    window.load = this.inicio();
  },
  computed: {
    ...mapGetters({
      imagen: 'imagen', clave: 'clave', blob: 'blob'
    }),
  },
  methods: {
    inicio() {
      window.fbq("track", "CompleteRegistration");
      console.log("All assets are loaded");
      setTimeout(() => {
        this.estatus = true;
        this.loading = false;
      }, 100);
    },
    facebook() {
      /*window.FB.ui({
        method: 'share_open_graph',
        action_type: 'og.shares',
        action_properties: JSON.stringify({
          object : {
            'og:url': "https://mario.juguetronmexico.mx/user.php?u="+this.clave,
            'og:title': "¡Mario necesita tu ayuda!",
            'og:description': "¡Bowser tomó Juguetron! No permitas que se salga con la suya.",
            'og:og:image:width': '434',
            'og:image:height': '263',
            'og:image': "https://mario.juguetronmexico.mx/credenciales/" +this.clave+".png"
          }
        })
      });*/
      window.FB.ui(
              {
                method: "share",
                href: "https://mario.juguetronmexico.mx/user.php?u="+this.clave
              },
              function(response) {
                console.log("compartido en facebook");
              }
      );
    },
    descargar() {
      const downloadLink = document.createElement("a");
      downloadLink.setAttribute("download", "credencial.png");
      const url = URL.createObjectURL(this.blob);
      downloadLink.setAttribute("href", url);
      downloadLink.click();
    },
    reset() {
      this.$router.push({name: 'Home'});
    },
  }
});
</script>
<style>
.fondo-mario {
  background-image: url(/img/fondoblack.png);
  background-repeat: repeat-y;
  background-size: 100%;
}
.v-application {
  background-color: transparent !important;
}
.video-container {
  max-height: 440px;
  height: 100vh;
}
.font-blink {
  font-family: "Blinker" !important;
}
.cursor {
  cursor: url(/img/cursor.png), auto !important;
}
</style>
