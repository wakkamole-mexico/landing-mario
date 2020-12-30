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
        <v-img style="max-width: 200px" src="/img/juguetron.png"></v-img>
      </v-app-bar>
      <v-content>
        <v-container
          fluid
          class="ma-0 pa-0"
          style="margin-top: -64px !important;"
        >
          <video-background
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
          <v-parallax dark src="/img/fondo.png" height="100vh">
            <v-container class="pa-0 ma-0" fluid style="height: 100vh">
              <v-row style="position: relative; z-index: 2;">
                <v-card
                  flat
                  style="width: 900px; height: 100%; margin: auto; background: transparent;"
                >
                  <v-card-text>
                    <v-row ref="titlebowser" class="white--text">
                      <v-col
                        cols="12"
                        class="text-center"
                        :class="
                          $vuetify.breakpoint.mdAndUp
                            ? 'display-2'
                            : 'display-1'
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
                </v-card>
                <v-card
                  flat
                  style="width: 900px; height: 100%; margin: auto; background: transparent;"
                >
                  <div
                    style="position: absolute; background-color: #BBB; filter: opacity(.8); width: 100%; height: 100%;"
                  ></div>
                  <v-card-text
                    class="ma-0 px-6 white--text text-center"
                    :class="
                      $vuetify.breakpoint.mdAndUp
                        ? 'headline py-6'
                        : 'title py-2'
                    "
                    style="filter: opacity(1);"
                  >
                    <v-row class="mt-4">
                      <v-col class="font-blink font-weight-light">
                        <vue-text-transition
                          v-if="false"
                          :show="showText"
                          name="test"
                          tag="p"
                          :interval="10"
                          :custom-class="[
                            { selector: ':nth-child(odd)', class: 'test_odd' }
                          ]"
                        >
                          Pero... ¿Qué está pasando? ¿Bowser? ¡Sí! ¡Es Bowser!
                          Ese villano que tanto nos complicó pasar de nivel en
                          el videojuego, ahora tomó todas nuestras Tiendas y
                          ¡está distorsionando todo con la data! Necesitamos de
                          tu ayuda para formar el Ejército Mario más grande del
                          mundo y retomar el control de Juguetron. Mario Bros
                          está listo, ¿Tú lo estás?
                        </vue-text-transition>
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
                          class="font-blink font-weight-black cursor"
                          x-large
                          @click="
                            $vuetify.goTo($refs.formularios, {
                              duration: 700,
                              offset: 0,
                              easing: 'easeInQuad'
                            })
                          "
                        >
                          ¡Sí, estoy listo!
                        </v-btn>
                      </v-col>
                    </v-row>
                  </v-card-text>
                </v-card>
              </v-row>
            </v-container>
          </v-parallax>

          <v-parallax dark src="/img/fondo.png" height="250"> </v-parallax>
          <v-container
            v-if="step == 1"
            ref="formularios"
            class="pa-0 ma-0 fondo-mario"
            fluid
            style="height: calc(100vh - 65px)"
          >
            <v-card class="transparent">
              <v-card-text class="pa-0">
                <v-list-item class="pa-0">
                  <v-img
                    src="/img/gif1.gif"
                    max-width="240px"
                    style="height: calc(100vh - 65px)"
                    class="hidden-sm-and-down"
                  ></v-img>
                  <v-list-item-content class="pa-6">
                    <v-row>
                      <v-col cols="8" class="offset-2 hidden-sm-and-down">
                        <div class="display-1 mb-4 white--text font-blink">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                      <v-col cols="12" class="hidden-md-and-up">
                        <div class="title white--text font-blink mb-0">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                    </v-row>
                    <v-card class="transparent mt-0 pt-0">
                      <v-card-text class="mt-0 pt-0">
                        <v-row>
                          <v-col
                            cols="1"
                            class="white--text offset-1 text-right align-self-center hidden-sm-and-down"
                          >
                          </v-col>
                          <v-col :cols="$vuetify.breakpoint.mdAndUp ? 8 : 12">
                            <v-row>
                              <v-col cols="12">
                                <div
                                  class="white--text font-blink"
                                  :class="
                                    $vuetify.breakpoint.mdAndUp
                                      ? 'headline'
                                      : 'subtitle-1'
                                  "
                                >
                                  1. ¡Regístrate y forma parte del Ejército
                                  Mario con tu credencial exclusiva!
                                </div>
                              </v-col>
                            </v-row>
                            <v-form ref="formJoin">
                              <v-row>
                                <v-col cols="12">
                                  <v-text-field
                                    :dense="$vuetify.breakpoint.smAndDown"
                                    :hide-details="
                                      $vuetify.breakpoint.smAndDown
                                    "
                                    v-model="formJoin.nombre"
                                    dark
                                    label="Nombre"
                                    outlined
                                    :rules="[rules.required]"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    :dense="$vuetify.breakpoint.smAndDown"
                                    :hide-details="
                                      $vuetify.breakpoint.smAndDown
                                    "
                                    v-model="formJoin.correo"
                                    dark
                                    label="E-mail"
                                    outlined
                                    :rules="[rules.required, rules.email]"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-dialog
                                    ref="dialog"
                                    v-model="modalFn"
                                    persistent
                                    width="290px"
                                  >
                                    <template v-slot:activator="{ on }">
                                      <v-text-field
                                        :dense="$vuetify.breakpoint.smAndDown"
                                        :hide-details="
                                          $vuetify.breakpoint.smAndDown
                                        "
                                        v-model="computedDateFormatted"
                                        dark
                                        label="Tu cumpleaños"
                                        hint="DÍA / MES / AÑO"
                                        persistent-hint
                                        outlined
                                        append-icon="mdi-cake-variant"
                                        readonly
                                        v-on="on"
                                        :rules="[rules.required]"
                                      ></v-text-field>
                                    </template>
                                    <v-date-picker
                                      ref="picker"
                                      v-model="formJoin.fechaNacimiento"
                                      :max="
                                        new Date().toISOString().substr(0, 10)
                                      "
                                      min="1950-01-01"
                                      @change="modalFn = false"
                                    ></v-date-picker>
                                  </v-dialog>
                                </v-col>
                              </v-row>
                              <v-row class="hidden-md-and-up">
                                <v-col
                                  cols="6"
                                  class="white--text text-left align-self-center"
                                >
                                  <v-btn class="ma-2" outlined fab color="teal">
                                    <v-icon>mdi-chevron-left</v-icon>
                                  </v-btn>
                                </v-col>
                                <v-col
                                  cols="6"
                                  class="white--text text-right align-self-center"
                                >
                                  <v-btn
                                    @click="join()"
                                    class="ma-2"
                                    outlined
                                    fab
                                    color="teal"
                                  >
                                    <v-icon>mdi-chevron-right</v-icon>
                                  </v-btn>
                                </v-col>
                              </v-row>
                            </v-form>
                          </v-col>
                          <v-col
                            cols="1"
                            class="white--text text-left align-self-center hidden-sm-and-down"
                          >
                            <v-btn
                              @click="join()"
                              class="ma-2"
                              outlined
                              fab
                              color="teal"
                            >
                              <v-icon>mdi-chevron-right</v-icon>
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
              src="/img/gif1h.gif"
              width="100%"
              class="hidden-md-and-up"
            ></v-img>
          </v-container>

          <v-container
            v-if="step == 2"
            class="pa-0 ma-0 fondo-mario"
            fluid
            style="height: calc(100vh - 65px)"
          >
            <v-card class="transparent">
              <v-card-text class="pa-0">
                <v-list-item class="pa-0">
                  <v-img
                    src="/img/gif2.gif"
                    max-width="240px"
                    style="height: calc(100vh - 65px)"
                    class="hidden-sm-and-down"
                  ></v-img>
                  <v-list-item-content class="pa-6">
                    <v-row>
                      <v-col cols="8" class="offset-2 hidden-sm-and-down">
                        <div class="display-1 mb-4 white--text font-blink">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                      <v-col cols="12" class="hidden-md-and-up">
                        <div class="title white--text font-blink mb-0">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                    </v-row>
                    <v-card class="transparent">
                      <v-card-text>
                        <v-row>
                          <v-col
                            cols="1"
                            class="white--text offset-1 text-right align-self-center hidden-sm-and-down"
                          >
                            <v-btn
                              @click="regresar(1)"
                              class="ma-2"
                              outlined
                              fab
                              color="teal"
                            >
                              <v-icon>mdi-chevron-left</v-icon>
                            </v-btn>
                          </v-col>
                          <v-col :cols="$vuetify.breakpoint.mdAndUp ? 8 : 12">
                            <v-row>
                              <v-col cols="12">
                                <div
                                  class="white--text font-blink"
                                  :class="
                                    $vuetify.breakpoint.mdAndUp
                                      ? 'headline'
                                      : 'subtitle-1'
                                  "
                                >
                                  2. ¡Estás a nada de formar parte del Ejército
                                  Mario!. Personaliza tu tarjeta
                                </div>
                              </v-col>
                            </v-row>
                            <v-row>
                              <v-col cols="12" class="hidden-sm-and-down">
                                <v-slide-group
                                  v-model="model"
                                  class="pa-4"
                                  mandatory
                                  show-arrows
                                  dark
                                  center-active
                                >
                                  <v-slide-item
                                    v-for="n in credenciales"
                                    :key="n.id"
                                    v-slot:default="{ active, toggle }"
                                  >
                                    <v-card
                                      :color="
                                        active ? 'primary' : 'grey lighten-1'
                                      "
                                      class="ma-4"
                                      height="140"
                                      width="250"
                                      @click="toggle"
                                    >
                                      <v-img
                                        :src="n.url"
                                        class="white--text align-end"
                                        gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                                        height="140px"
                                      >
                                        <v-scale-transition>
                                          <v-icon
                                            v-if="active"
                                            color="white"
                                            size="48"
                                            v-text="'mdi-check-circle-outline'"
                                          ></v-icon>
                                        </v-scale-transition>
                                      </v-img>
                                    </v-card>
                                  </v-slide-item>
                                </v-slide-group>
                              </v-col>
                              <v-col cols="12" class="hidden-md-and-up">
                                <v-item-group
                                  v-model="model"
                                  active-class="primary"
                                >
                                  <v-container>
                                    <v-row>
                                      <v-col
                                        v-for="n in credenciales"
                                        :key="n.id"
                                        cols="12"
                                      >
                                        <v-item
                                          v-slot:default="{ active, toggle }"
                                        >
                                          <v-card
                                            class="d-flex align-center"
                                            dark
                                            @click="toggle"
                                          >
                                            <v-img
                                              :src="n.url"
                                              class="white--text align-end"
                                              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                                            >
                                              <v-scale-transition>
                                                <v-icon
                                                  v-if="active"
                                                  color="white"
                                                  size="48"
                                                  v-text="
                                                    'mdi-check-circle-outline'
                                                  "
                                                ></v-icon>
                                              </v-scale-transition>
                                            </v-img>
                                          </v-card>
                                        </v-item>
                                      </v-col>
                                    </v-row>
                                  </v-container>
                                </v-item-group>
                              </v-col>
                            </v-row>
                            <v-row class="hidden-md-and-up">
                              <v-col
                                cols="6"
                                class="white--text text-left align-self-center"
                              >
                                <v-btn
                                  @click="regresar(1)"
                                  class="ma-2"
                                  outlined
                                  fab
                                  color="teal"
                                >
                                  <v-icon>mdi-chevron-left</v-icon>
                                </v-btn>
                              </v-col>
                              <v-col
                                cols="6"
                                class="white--text text-right align-self-center"
                              >
                                <v-btn
                                  @click="elegir()"
                                  class="ma-2"
                                  outlined
                                  fab
                                  color="teal"
                                >
                                  <v-icon>mdi-chevron-right</v-icon>
                                </v-btn>
                              </v-col>
                            </v-row>
                          </v-col>
                          <v-col
                            cols="1"
                            class="white--text offset-1 text-right align-self-center hidden-sm-and-down"
                          >
                            <v-btn
                              @click="elegir()"
                              class="ma-2"
                              outlined
                              fab
                              color="teal"
                            >
                              <v-icon>mdi-chevron-right</v-icon>
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
              src="/img/gif2h.gif"
              width="100%"
              class="hidden-md-and-up"
            ></v-img>
          </v-container>

          <v-container
            v-if="step == 3"
            class="pa-0 ma-0 fondo-mario"
            fluid
            style="height: calc(100vh - 65px)"
          >
            <v-card class="transparent">
              <v-card-text class="pa-0">
                <v-list-item class="pa-0">
                  <v-img
                    src="/img/gif3.gif"
                    max-width="240px"
                    style="height: calc(100vh - 65px)"
                    class="hidden-sm-and-down"
                  ></v-img>
                  <v-list-item-content class="pa-6">
                    <v-row>
                      <v-col cols="8" class="offset-2 hidden-sm-and-down">
                        <div class="display-1 mb-4 white--text font-blink">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                      <v-col cols="12" class="hidden-md-and-up">
                        <div class="title white--text font-blink mb-0">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                    </v-row>
                    <v-card class="transparent">
                      <v-card-text>
                        <v-row>
                          <v-col
                            cols="1"
                            class="white--text offset-1 text-right align-self-center hidden-sm-and-down"
                          >
                            <v-btn
                              @click="regresar(2)"
                              class="ma-2"
                              outlined
                              fab
                              color="teal"
                            >
                              <v-icon>mdi-chevron-left</v-icon>
                            </v-btn>
                          </v-col>
                          <v-col :cols="$vuetify.breakpoint.mdAndUp ? 8 : 12">
                            <v-form ref="formUsername">
                              <v-row>
                                <v-col cols="12">
                                  <div
                                    class="white--text font-blink"
                                    :class="
                                      $vuetify.breakpoint.mdAndUp
                                        ? 'headline'
                                        : 'subtitle-1'
                                    "
                                  >
                                    3. ¡Estás a nada de formar parte del
                                    Ejército Mario! Define tu Username.
                                  </div>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    :dense="$vuetify.breakpoint.smAndDown"
                                    :hide-details="
                                      $vuetify.breakpoint.smAndDown
                                    "
                                    v-model="username"
                                    counter
                                    maxlength="14"
                                    :rules="[rules.required, rules.max(14)]"
                                    dark
                                    label="¿Nombre para tu credencial?"
                                    outlined
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                              <v-row class="hidden-md-and-up">
                                <v-col
                                  cols="6"
                                  class="white--text text-left align-self-center"
                                >
                                  <v-btn
                                    @click="regresar(2)"
                                    class="ma-2"
                                    outlined
                                    fab
                                    color="teal"
                                  >
                                    <v-icon>mdi-chevron-left</v-icon>
                                  </v-btn>
                                </v-col>
                                <v-col
                                  cols="6"
                                  class="white--text text-right align-self-center"
                                >
                                  <v-btn
                                    @click="setUsername()"
                                    class="ma-2"
                                    outlined
                                    fab
                                    color="teal"
                                  >
                                    <v-icon>mdi-chevron-right</v-icon>
                                  </v-btn>
                                </v-col>
                              </v-row>
                            </v-form>
                          </v-col>
                          <v-col
                            cols="1"
                            class="white--text text-left align-self-center hidden-sm-and-down"
                          >
                            <v-btn
                              @click="setUsername()"
                              class="ma-2"
                              outlined
                              fab
                              color="teal"
                            >
                              <v-icon>mdi-chevron-right</v-icon>
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
              src="/img/gif3h.gif"
              width="100%"
              class="hidden-md-and-up"
            ></v-img>
          </v-container>

          <v-container
            v-if="step == 4"
            class="pa-0 ma-0 fondo-mario"
            fluid
            style="height: calc(100vh - 65px)"
          >
            <v-card class="transparent">
              <v-card-text class="pa-0">
                <v-list-item class="pa-0">
                  <v-img
                    src="/img/gif4.gif"
                    max-width="240px"
                    style="height: calc(100vh - 65px)"
                    class="hidden-sm-and-down"
                  ></v-img>
                  <v-list-item-content class="pa-6">
                    <v-row>
                      <v-col cols="8" class="offset-2 hidden-sm-and-down">
                        <div class="display-1 mb-4 white--text font-blink">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                      <v-col cols="12" class="hidden-md-and-up">
                        <div class="title white--text font-blink mb-0">
                          OBTÉN TU CREDENCIAL EXCLUSIVA Y ÚNICA DEL EJÉRCITO
                          MARIO
                        </div>
                      </v-col>
                    </v-row>
                    <v-card class="transparent">
                      <v-card-text>
                        <v-row>
                          <v-col
                            cols="1"
                            class="white--text offset-1 text-right align-self-center hidden-sm-and-down"
                          >
                            <v-btn
                              @click="regresar(3)"
                              class="ma-2"
                              outlined
                              fab
                              color="teal"
                            >
                              <v-icon>mdi-chevron-left</v-icon>
                            </v-btn>
                          </v-col>
                          <v-col :cols="$vuetify.breakpoint.mdAndUp ? 8 : 12">
                            <v-row>
                              <v-col cols="12">
                                <div
                                  class="white--text font-blink"
                                  :class="
                                    $vuetify.breakpoint.mdAndUp
                                      ? 'headline'
                                      : 'subtitle-1'
                                  "
                                >
                                  4. ¡Casi lo logras!. Sube tu fotografía.
                                </div>
                              </v-col>
                            </v-row>
                            <v-row>
                              <v-col cols="12" class="text-center">
                                <div>Sube tu fotografía</div>
                                <v-hover v-slot:default="{ hover }">
                                  <v-avatar size="250">
                                    <v-img
                                      class="custom-vimg"
                                      :eager="true"
                                      :src="'/img/marioperfil.png'"
                                    >
                                      <v-expand-transition>
                                        <div
                                          v-if="true"
                                          class="d-flex transition-fast-in-fast-out blue-grey darken-4 v-card--reveal display-3 white--text"
                                          style="height: 100%;"
                                        >
                                          <v-btn
                                            icon
                                            color="white"
                                            @click="openImagen()"
                                          >
                                            <v-icon
                                              x-large
                                              :class="{ 'show-btns': hover }"
                                            >
                                              mdi-camera
                                            </v-icon>
                                          </v-btn>
                                        </div>
                                      </v-expand-transition>
                                    </v-img>
                                  </v-avatar>
                                </v-hover>
                              </v-col>
                            </v-row>
                            <v-row class="hidden-md-and-up">
                              <v-col
                                cols="6"
                                class="white--text text-left align-self-center"
                              >
                                <v-btn
                                  @click="regresar(3)"
                                  class="ma-2"
                                  outlined
                                  fab
                                  color="teal"
                                >
                                  <v-icon>mdi-chevron-left</v-icon>
                                </v-btn>
                              </v-col>
                              <v-col
                                cols="6"
                                class="white--text text-right align-self-center"
                              >
                                <v-btn
                                  @click="finalizar()"
                                  class="ma-2"
                                  outlined
                                  fab
                                  color="teal"
                                >
                                  <v-icon>mdi-chevron-right</v-icon>
                                </v-btn>
                              </v-col>
                            </v-row>
                          </v-col>
                          <v-col
                            cols="1"
                            class="white--text text-left align-self-center hidden-sm-and-down"
                          >
                            <v-btn
                              @click="finalizar()"
                              class="ma-2"
                              outlined
                              fab
                              color="teal"
                            >
                              <v-icon>mdi-chevron-right</v-icon>
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
              src="/img/gif4h.gif"
              width="100%"
              class="hidden-md-and-up"
            ></v-img>
          </v-container>

          <v-container
            v-if="step == 5"
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
                              :src="imagenPrev"
                            />
                          </v-col>
                          <v-col cols="12" class="text-center">
                            <v-btn @click="reset()">Regresar</v-btn>
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
            ></v-img>
          </v-container>
        </v-container>
      </v-content>
    </template>
    <v-dialog
      v-model="dialogImg"
      :fullscreen="$vuetify.breakpoint.mdAndUp ? false : true"
      scrollable
      max-width="900px"
    >
      <v-card>
        <v-toolbar style="background-color: #2BCBFB" dark>
          <v-toolbar-title class="ml-0 pl-4">
            <span class="hidden-sm-and-down"
              >Sube tu fotografía para tu credencial</span
            >
            <span class="hidden-md-and-up">Sube tu foto</span>
          </v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon dark @click="closeImagen()">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-toolbar>
        <v-card-text>
          <v-form ref="formImagen">
            <v-row>
              <v-file-input
                :rules="[rules.required, rules.size]"
                accept="image/png, image/jpeg, image/bmp"
                placeholder="Selecciona una imagen de tu equipo"
                prepend-icon="mdi-camera"
                label="Imagen de grupo"
                v-model="selectedFile"
                :show-size="1024"
                @change="setupCropper"
              ></v-file-input>
            </v-row>
            <v-row v-if="objectUrl">
              <v-col
                :cols="$vuetify.breakpoint.mdAndUp ? '6' : '12'"
                class="text-center"
              >
                <div class="image-container elevation-4">
                  <img class="image-preview" ref="source" :src="objectUrl" />
                </div>
                <div class="d-flex justify-center">
                  <v-btn icon="icon" small="small" @click="resetCropper">
                    <v-icon small="small">mdi-aspect-ratio</v-icon>
                  </v-btn>
                  <div class="mx-2"></div>
                  <v-btn icon="icon" small="small" @click="rotateLeft">
                    <v-icon small="small">mdi-rotate-left</v-icon>
                  </v-btn>
                  <v-btn icon="icon" small="small" @click="rotateRight">
                    <v-icon small="small">mdi-rotate-right</v-icon>
                  </v-btn>
                </div>
              </v-col>
              <v-col :cols="$vuetify.breakpoint.mdAndUp ? '6' : '12'">
                <div
                  ref="credencial"
                  style="position: relative; width: 100%; height: 100%"
                >
                  <img src="/img/credencial_base.png" style="width: 100%;" />
                  <div style="position: absolute; top: 0px; z-index: 2;">
                    <img :src="credenciales[model].url" style="width: 100%;" />
                  </div>
                  <div
                    class="font-blink black--text"
                    style="position: absolute; z-index: 3; bottom: 13px; left: 15px; font-weight: bold;"
                  >
                    {{ matricula }}
                  </div>
                  <div
                    class="font-blink"
                    :class="model == 2 ? 'black--text' : 'white--text'"
                    style="position: absolute; z-index: 3; font-size: 1.8em; line-height: 1.5em; text-align: center; width: 50%; bottom: 25%; left: 40%; font-weight: bold;"
                  >
                    {{ username }}
                  </div>
                  <div style="width: 33%; position:absolute; top: 0px;">
                    <img
                      style="width: 100%; border-radius: 20px; margin-left: 29px; margin-top: 42px;"
                      :src="previewCropped"
                    />
                  </div>
                </div>
              </v-col>
              <v-col cols="12">
                <div ref="prevcred" style="width: 100%;"></div>
              </v-col>
            </v-row>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="closeImagen()"
            >Cancelar</v-btn
          >
          <v-btn color="blue darken-1" text @click="subirImagen()"
            >Guardar</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VideoBackground from "vue-responsive-video-background-player";
import VueTextTransition from "vue-text-transition";
import { RULES } from "./mixins/rules";
import { CROPPER } from "./mixins/cropper";
import html2canvas from "html2canvas";
import VScrollin from "vue-scrollin";
import Glitch from "vue-glitch";

export default Vue.extend({
  name: "App",
  mixins: [CROPPER, RULES],
  components: {
    VideoBackground,
    VueTextTransition,
    VScrollin,
    Glitch
  },
  data: () => ({
    modalFn: false,
    model: null,
    estatus: false,
    loading: true,
    dialogImg: false,
    showTitle: false,
    showText: false,
    elements: null,
    toRotate: [],
    el: null,
    loopNum: 0,
    period: 0,
    txt: "",
    isDeleting: false,
    step: 1,
    credenciales: [
      { id: 1, url: "/img/credencial1.png" },
      { id: 2, url: "/img/credencial2.png" },
      { id: 3, url: "/img/credencial3.png" }
    ],
    credencialActiva: null,
    id: null,
    formJoin: {
      nombre: "",
      correo: "",
      fechaNacimiento: ""
    },
    username: "",
    matricula: "",
    image: null,
    imagenPrev: null,
    scroll: 0
  }),
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  mounted() {
    window.addEventListener("load", () => {
      console.log("All assets are loaded");
      setTimeout(() => {
        this.estatus = true;
        this.loading = false;
        setTimeout(() => {
          this.showTitle = true;
          this.elements = document.getElementsByClassName("txt-rotate");
          console.log(this.elements[0]);
          for (let i = 0; i < this.elements.length; i++) {
            const toRotate = this.elements[i].getAttribute("data-rotate");
            const period = this.elements[i].getAttribute("data-period");
            console.log(this.elements[i]);
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
      }, 100);
    });
  },
  computed: {
    pageHeight() {
      return document.body.scrollHeight;
    },
    computedDateFormatted() {
      return this.formatDate(this.formJoin.fechaNacimiento);
    }
  },
  watch: {
    modalFn(val) {
      val && this.$nextTick(() => (this.$refs.picker.activePicker = "YEAR"));
    }
  },
  methods: {
    reset() {
      this.step = 1;
      this.credencialActiva = null;
      this.id = null;
      this.formJoin = {
        nombre: "",
        correo: "",
        fechaNacimiento: ""
      };
      this.username = "";
      this.matricula = "";
      this.image = null;
      this.imagenPrev = null;
      this.$vuetify.goTo(0, {
        duration: 700,
        offset: 0,
        easing: "easeInQuad"
      });
    },
    formatDate(date) {
      if (!date) return null;
      const [year, month, day] = date.split("-");
      return `${day}/${month}/${year}`;
    },
    finalizar() {
      this.loading = true;
      const formData = new FormData();
      formData.append("picture", this.image, "picture.png");
      formData.append("id", this.id);
      axios
        .post("/functions/credencial.php", formData, {
          "Content-Type": "multipart/form-data"
        })
        .then(response => {
          console.log(response.data);
        })
        .catch(err => {
          this.loading = false;
        })
        .finally(() => {
          this.loading = false;
        });
      this.step = 5;
    },
    setUsername() {
      if (this.$refs.formUsername.validate()) {
        this.step = 4;
      }
    },
    elegir(cred) {
      this.step = 3;
    },
    regresar(n) {
      this.step = n;
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
        offset: 20,
        easing: "easeInQuad"
      });
      this.showText = true;
    },
    join() {
      if (this.$refs.formJoin.validate()) {
        this.loading = true;
        this.matricula = "A20-9999";
        setTimeout(() => {
          axios
            .post(
              "http://mario.juguetronmexico.mx/functions/save.php",
              this.formJoin
            )
            .then(response => {
              console.log(response.data);
            })
            .catch(err => {
              this.loading = false;
            })
            .finally(() => {
              this.loading = false;
            });
          this.step = 2;
        }, 500);
      } else {
        console.log("errores en formulario");
      }
    },
    subirImagen() {
      console.log(this.$refs.credencial);
      const area = this.$refs.credencial.getBoundingClientRect();
      this.loading = true;
      html2canvas(this.$refs.credencial, {
        scrollX: 0,
        scrollY: 0,
        width: area.width,
        height: area.height,
        backgroundColor: null,
        removeContainer: true
      })
        .then(canvas => {
          //console.log(canvas.toDataURL("image/jpg"));
          const downloadLink = document.createElement("a");
          downloadLink.setAttribute("download", "credencial.png");
          this.imagenPrev = canvas.toDataURL("image/png");
          canvas.toBlob(blob => {
            const url = URL.createObjectURL(blob);
            downloadLink.setAttribute("href", url);
            //downloadLink.click();
            this.image = blob;
            this.dialogImg = false;
            this.loading = false;
            this.finalizar();
          });
        })
        .catch(error => {
          this.loading = false;
          console.log("ERROR SAVING IMAGE", error);
        });
    },
    openImagen() {
      this.previewImagen = null;
      this.zoomable = true;
      //this.radio = 4/5;
      this.radio = 1;
      this.dialogImg = true;
    },
    closeImagen() {
      this.selectedFile = undefined;
      this.setupCropper(undefined);
      this.uploadPercentage = 0;
      this.dialogImg = false;
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
<style lang="sass" scoped>
.image-container
  display: inline-block

  .image-preview
    display: block
    max-height: 229px
    max-width: 100%
</style>
<style>
.custom-vimg .v-image__image--cover {
  background-size: contain !important;
}
.no-active {
  color: rgba(0, 0, 0, 0.54) !important;
}
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: 0.5;
  position: absolute;
  width: 100%;
}
</style>
