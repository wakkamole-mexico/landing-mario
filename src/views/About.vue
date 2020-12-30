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
                            <v-btn
                              @click="$router.push({ name: 'Home' })"
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
                                  1. ¡Regístrate y forma parte del Ejército
                                  Mario con tu credencial exclusiva!
                                </div>
                              </v-col>
                            </v-row>
                            <v-row v-if="error!=''">
                              <v-col cols="12" class="font-blink white--text title">
                                {{error}}
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
                              <v-row class="hidden-md-and-up mb-12">
                                <v-col
                                  cols="6"
                                  class="white--text text-left align-self-center"
                                >
                                  <v-btn
                                    @click="$router.push({ name: 'Home' })"
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
              style="position: fixed; bottom: 0px;"
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
                                  Mario! Personaliza tu tarjeta.
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
                            <v-row class="hidden-md-and-up mb-12">
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
              style="position: fixed; bottom: 0px;"
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
                                    3. ¡Vamos!, Te falta poco. Define tu Username.
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
                              <v-row class="hidden-md-and-up mb-12">
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
              style="position: fixed; bottom: 0px;"
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
                            <v-row class="hidden-md-and-up mb-12">
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
              style="position: fixed; bottom: 0px;"
            ></v-img>
          </v-container>

        </v-container>
      </v-content>
    </template>
    <v-dialog
      v-model="dialogImg"
      :fullscreen="$vuetify.breakpoint.smAndDown"
      :scrollable="$vuetify.breakpoint.mdAndUp"
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
              <v-col>
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
              </v-col>
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
                    :style="
                      $vuetify.breakpoint.smAndDown
                        ? 'bottom: 13px; left: 15px;'
                        : 'bottom: 6%; left: 4%;'
                    "
                    style="position: absolute; z-index: 3; font-weight: bold;"
                  >
                    {{ matricula }}
                  </div>
                  <div
                    class="font-blink"
                    :class="model == 2 ? 'black--text' : 'white--text'"
                    :style="
                      $vuetify.breakpoint.smAndDown
                        ? 'bottom: 25%; left: 40%;'
                        : 'bottom: 30%; left: 40%;'
                    "
                    style="position: absolute; z-index: 3; font-size: 1.8em; line-height: 1.5em; text-align: center; width: 60%; font-weight: bold;"
                  >
                    {{ username }}
                  </div>
                  <div style="width: 33%; position:absolute; top: 0px;">
                    <img
                      style="width: 100%; border-radius: 20px; margin-left: 21%; margin-top: 32%;"
                      :src="previewCropped"
                    />
                  </div>
                </div>
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
import axios from "axios";
import { RULES } from "../mixins/rules";
import { CROPPER } from "../mixins/cropper";
import html2canvas from "html2canvas";

export default Vue.extend({
  name: "App",
  mixins: [CROPPER, RULES],
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
    scroll: 0,
    downloadLink: null,
    error: '',
  }),
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  mounted() {
    window.load = this.inicio();
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
    inicio() {
      console.log("All assets are loaded");
      setTimeout(() => {
        this.estatus = true;
        this.loading = false;
      }, 100);
    },
    formatDate(date) {
      if (!date) return null;
      const [year, month, day] = date.split("-");
      return `${day}/${month}/${year}`;
    },
    finalizar() {
      if (this.id != null) {
        this.loading = true;
        const formData = new FormData();
        formData.append("userfile", this.image, "picture.png");
        formData.append("id_lead", this.id);
        axios
          .post("/functions/credencial.php", formData, {
            "Content-Type": "multipart/form-data"
          })
          .then(response => {
            if (response.data.result) {
              this.$store.dispatch('updateData',{imagen: this.imagenPrev, clave: this.matricula, blob: this.image});
              this.$router.push({name: 'Thanks'});
            }
          })
          .catch(err => {
            this.loading = false;
          })
          .finally(() => {
            this.loading = false;
          });
      }
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
      this.error = '';
      if (this.$refs.formJoin.validate()) {
        this.loading = true;
        this.matricula = "A20-9999";
        setTimeout(() => {
          axios
            .post("/functions/save.php", {
              email: this.formJoin.correo,
              name: this.formJoin.nombre,
              birthday: this.formJoin.fechaNacimiento
            })
            .then(response => {
              if (response.data.result) {
                this.id = response.data.id;
                this.matricula = response.data.clave;
                this.step = 2;
              }else{
                this.error = response.data.msg;
              }
            })
            .catch(err => {
              this.loading = false;
            })
            .finally(() => {
              this.loading = false;
            });
        }, 500);
      } else {
        console.log("errores en formulario");
      }
    },
    subirImagen() {
      const area = this.$refs.credencial.getBoundingClientRect();
      this.loading = true;
      html2canvas(this.$refs.credencial, {
        scrollX: 0,
        scrollY: 0,
        width: area.width + 20,
        height: area.height,
        backgroundColor: null,
        removeContainer: true
      })
        .then(canvas => {
          this.imagenPrev = canvas.toDataURL("image/png");
          canvas.toBlob(blob => {
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
      this.radio = 1;
      this.dialogImg = true;
    },
    closeImagen() {
      this.selectedFile = undefined;
      this.setupCropper(undefined);
      this.uploadPercentage = 0;
      this.dialogImg = false;
    },
  }
});
</script>
<style>
body {
  font-family: "Blinker" !important;
}
.fondo-mario {
  background-image: url(/img/fondoblack.png);
  background-repeat: repeat-y;
  background-size: 100%;
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
