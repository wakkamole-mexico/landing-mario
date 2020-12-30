<template>
  <v-app class="cursor">
    <div
      v-if="false"
      style="position: fixed; background-color: #FFF; top: 0; z-index: 9999"
    >
      {{ this.scroll }}
    </div>
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
      <v-app-bar app flat class="transparent">
        <v-img style="max-width: 150px" src="/img/lego-mario.png"></v-img>
        <v-spacer />
        <v-img v-if="false" style="max-width: 200px" src="/img/juguetron.png"></v-img>
      </v-app-bar>
      <v-content>
        <v-container fluid class="ma-0 pa-0">
          <v-container ref="formularios" class="pa-0 ma-0" fluid>
            <v-card class="ma-0 pa-0 transparent" flat>
              <v-row class="ma-0 pa-0">
                <v-col class="ma-0 pa-0">
                  <video-background
                    style="margin-top: -65px;"
                    class="video-container"
                    src="/video/mario.mp4"
                    :sources="[
                      { src: '/video/mariofull.mp4', res: 991, autoplay: true },
                      {
                        src: '/video/mariomobile.mp4',
                        res: 575,
                        autoplay: true
                      }
                    ]"
                  >
                  </video-background>
                </v-col>
              </v-row>
              <v-card-text>
                <v-row ref="titlebowser" class="white--text">
                  <v-col
                    cols="12"
                    class="text-center"
                    :class="
                      $vuetify.breakpoint.mdAndUp ? 'display-2' : 'display-1'
                    "
                  >
                    <div class="font-blink font-weight-thin">
                      <VScrollin :speed="30">
                        ¡Bowser tomó Juguetron!
                      </VScrollin>
                    </div>
                  </v-col>
                  <v-col cols="12" class="text-center headline">
                    <span
                      class="txt-rotate font-blink font-weight-thin"
                      style="font-size: 1em;"
                      data-period="1000"
                      data-rotate='[ "No permitas que se salga con la suya.", "¡Necesitamos ayuda!"]'
                    ></span>
                  </v-col>
                  <v-col cols="12" class="text-center">
                    <v-btn
                      class="ma-2"
                      outlined
                      fab
                      color="teal"
                      @click="animateText()"
                    >
                      <v-icon>mdi-chevron-down</v-icon>
                    </v-btn>
                  </v-col>
                </v-row>
              </v-card-text>
              <v-card-text>
                <v-row>
                  <v-col>
                    <v-card
                      flat
                      style="width: 900px; height: 100%; margin: auto; background: transparent;"
                    >
                      <div
                        style="position: absolute; background-color: #BBB; filter: opacity(.8); width: 100%; height: 100%;"
                      ></div>
                      <v-card-text
                        class="ma-0 white--text text-center"
                        :class="
                          $vuetify.breakpoint.mdAndUp ? 'headline' : 'title'
                        "
                        style="filter: opacity(1);"
                      >
                        <v-row>
                          <v-col class="font-blink font-weight-light">
                            <glitch
                              text="Pero... ¿Qué está pasando? ¿Bowser? ¡Sí! ¡Es Bowser!
                          Ese villano que tanto nos complicó pasar de nivel en
                          el videojuego, ahora tomó todas nuestras Tiendas y
                          ¡está distorsionando todo con la data! Necesitamos de
                          tu ayuda para formar el Ejército Mario más grande del
                          mundo y retomar el control de Juguetron. Mario Bros
                          está listo, ¿Tú lo estás?"
                              background="transparent"
                            ></glitch>
                          </v-col>
                        </v-row>
                        <v-row>
                          <v-col class="text-center">
                            <v-btn
                              ref="btnForm"
                              class="font-blink font-weight-black cursor"
                              x-large
                              @click="goForm()"
                            >
                              ¡Sí, estoy listo!
                            </v-btn>
                          </v-col>
                        </v-row>
                      </v-card-text>
                    </v-card>
                  </v-col>
                </v-row>
              </v-card-text>
            </v-card>
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
import VideoBackground from "vue-responsive-video-background-player";
//import VueTextTransition from "vue-text-transition";
import { RULES } from "../mixins/rules";
import { CROPPER } from "../mixins/cropper";
import VScrollin from "vue-scrollin";
import Glitch from "vue-glitch";

export default Vue.extend({
  name: "App",
  mixins: [CROPPER, RULES],
  components: {
    VideoBackground,
    //VueTextTransition,
    VScrollin,
    Glitch
  },
  data: () => ({
    estatus: false,
    loading: true,
    showTitle: false,
    showText: false,
    elements: null,
    toRotate: [],
    el: null,
    loopNum: 0,
    period: 0,
    txt: "",
    isDeleting: false,
    scroll: 0
  }),
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  mounted() {
    window.onload = this.inicio();
    this.$store.dispatch('updateData',{imagen: null, clave: null, blob: null});
  },
  computed: {
    pageHeight() {
      return document.body.scrollHeight;
    }
  },
  watch: {},
  methods: {
    inicio() {
      console.log("All assets are loaded");
      setTimeout(() => {
        this.estatus = true;
        this.loading = false;
        setTimeout(() => {
          this.showTitle = true;
          this.elements = document.getElementsByClassName("txt-rotate");
          for (let i = 0; i < this.elements.length; i++) {
            const toRotate = this.elements[i].getAttribute("data-rotate");
            const period = this.elements[i].getAttribute("data-period");
            if (toRotate) {
              this.TxtRotate(this.elements[i], JSON.parse(toRotate), period);
            }
          }
          // INJECT CSS
          const css = document.createElement("style");
          css.type = "text/css";
          css.innerHTML =
            ".txt-rotate > .wrap { border-right: 0.08em solid #666 }";
          document.body.appendChild(css);
        }, 100);
      }, 1000);
    },
    goForm() {
      this.$vuetify
        .goTo(0, {
          duration: 700,
          offset: 0,
          easing: "easeInQuad"
        })
        .then(() => {
          this.$router.push({ name: "About" });
        });
    },
    handleScroll(e) {
      this.scroll = window.scrollY || window.scrollTop;
      if (this.scroll > 0 && !this.showText) {
        this.showText = true;
      }
    },
    animateText() {
      this.$vuetify.goTo(this.$refs.titlebowser, {
        duration: 700,
        offset: 10,
        easing: "easeInQuad"
      });
      this.showText = true;
    },
    tick() {
      const i = this.loopNum % this.toRotate.length;
      const fullTxt = this.toRotate[i];

      if (this.isDeleting) {
        this.txt = fullTxt.substring(0, this.txt.length - 1);
      } else {
        this.txt = fullTxt.substring(0, this.txt.length + 1);
      }

      this.el.innerHTML = '<span class="wrap">' + this.txt + "</span>";

      let delta = 300 - Math.random() * 100;

      if (this.isDeleting) {
        delta /= 2;
      }

      if (!this.isDeleting && this.txt === fullTxt) {
        delta = this.period;
        this.isDeleting = true;
      } else if (this.isDeleting && this.txt === "") {
        this.isDeleting = false;
        this.loopNum++;
        delta = 500;
      }

      setTimeout(() => {
        this.tick();
      }, delta);
    },
    TxtRotate(el, toRotate, period) {
      this.toRotate = toRotate;
      this.el = el;
      this.loopNum = 0;
      this.period = parseInt(period, 10) || 2000;
      this.txt = "";
      this.tick();
      this.isDeleting = false;
    }
  }
});
</script>
<style>
.v--vtt-test,
.v--vtt-test_odd {
  will-change: transform, opacity;
  transition: opacity 0.3s ease-in-out, transform 1s ease-in-out;
}

.v--vtt-test_visible,
.v--vtt-test_odd_visible {
  opacity: 1;
  transform: translateY(0);
}

.v--vtt-test_hidden {
  opacity: 0;
  transform: translateY(20px);
}

.v--vtt-test_odd_hidden {
  opacity: 0;
  transform: translateY(-20px);
}
body {
  font-family: "Blinker" !important;
  background-image: url(/img/fondoblack.png);
  background-repeat: repeat-y;
  background-size: 100%;
}
.v-parallax__image-container {
  left: -1px !important;
}
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
