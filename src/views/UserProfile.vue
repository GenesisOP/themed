<template>
  <v-container
    id="user-profile-view"
    fluid
    tag="section"
  >
    <v-row justify="center">
      <v-col
        cols="12"
        md="10"
      >
      <material-card
          color="primary"
          icon="mdi-file-document"
        >
          <template #title>
            Cuestionario — <small class="text-body-1">Completa con tus datos</small>
          </template>
          <v-form>
            <v-container class="py-0">
              <v-row>
                <v-col
                  cols="12"
                  class="text-center"
                >
                  <v-stepper v-model="e1">
      <v-stepper-header>
        <v-stepper-step
          :complete="e1 > 1"
          step="1"
        >
          Datos Generales
        </v-stepper-step>
        <v-divider></v-divider>
        <v-stepper-step
          :complete="e1 > 2"
          step="2"
        >
          Datos fiscales
        </v-stepper-step>
        <v-divider></v-divider>
        <v-stepper-step step="3">
          Datos Cofepris
        </v-stepper-step>
        <v-divider></v-divider>
        <v-stepper-step step="4">
          Final
        </v-stepper-step>
      </v-stepper-header>
      <v-stepper-items>
        <v-stepper-content step="1">
          <v-row>
                <v-col
                  cols="4"
                  md="2"
                >
                  <v-text-field
                    color="purple"
                    label="Titulo"
                    filled
                    hide-details
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    label="Nombre(s)"
                    filled
                    hide-details
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Apellido Paterno"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Apellido Materno"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="6"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Especialidad(es)"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="6"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Otra (subespecialidad o diplomado)"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Telefono"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="8"
                  >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Correo electrónico"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Estado"
                    type="number"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Municipio"
                    type="number"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Ciudad"
                    type="number"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="6"
                >
                      <v-menu
                        ref="menu"
                        v-model="menu"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                      >
                        <template v-slot:activator="{ on, attrs }">
                          <v-text-field
                            v-model="date"
                            label="Fecha de nacimiento"
                            prepend-icon="mdi-calendar"
                            hide-details
                            readonly
                            filled
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          v-model="date"
                          :active-picker.sync="activePicker"
                          :max="(new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10)"
                          min="1950-01-01"
                          @change="save"
                        ></v-date-picker>
                      </v-menu>
              </v-col>
                <v-col
                  cols="12"
                  md="6"
                >
                <p class="text-left">{{ radios || 'Genero' }}</p>
                <v-radio-group
                    v-model="row"
                    hide-details
                    row
                  >
                    <v-radio
                      label="Masculino"
                      value="radio-1"
                    ></v-radio>
                    <v-radio
                      label="Femenino"
                      value="radio-2"
                    ></v-radio>
                    <v-radio
                      label="Otros"
                      value="radio-3"
                    ></v-radio>
                  </v-radio-group>
                </v-col>
          </v-row>
          <v-btn
            color="primary"
            @click="e1 = 2"
          >
            Continue
          </v-btn>
        </v-stepper-content>
        <v-stepper-content step="2">
          <!--   -------------------------Persona fisica y moral------------------ -->
          <v-tabs
            v-model="tabs"
            centered
          >
            <v-tab>Persona fisica</v-tab>
            <v-tab>Persona moral</v-tab>
          </v-tabs>
      <v-tabs-items v-model="tabs">
        <v-tab-item>
          <v-row>
            <br>
              <v-col
                  cols="12"
                  md="6"
                >
                  <v-text-field
                  hide-details
                    color="purple"
                    label="Nombre(s)"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Apellido paterno"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                    color="purple"
<<<<<<< HEAD
                    hide-details
=======
>>>>>>> ef49abf8d926a0e1cb3c7b259d1248bac6fe5f17
                    label="Apellido materno"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="RFC Persona Física"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="CURP"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Correo electrónico fiscal"
                    filled
                  />
                </v-col>
<<<<<<< HEAD
=======
               <!--  <v-col
                  cols="12"
                  md="6"
                >
                <p class="text-left">{{ radios || '¿Cuenta con Constancia de Situación Fiscal actualizada?' }}</p>
                
                <v-radio-group
                    v-model="row"
                    row
                  >
                    <v-radio
                      label="Si"
                    
                      @click="expand = !expand"
             
    
                      
                    ></v-radio>

                    <v-radio
                      label="No"
                      @click="isdeleted"
                    ></v-radio>

                    <v-radio
                      label="En trámite"
              
                    ></v-radio>
                  </v-radio-group>
                </v-col>

                <v-col 
                 
                  cols="12"
                  md="6"
                >

                <v-file-input 
                v-show="expand"
                    label="Subir Constancia de Situación Fiscal actualizada (PDF)"
                    outlined
                    dense
                  ></v-file-input>
                </v-col> -->
                
              
                <v-card-text>
                  <p class="text-CENTER">{{ radios || '¿Cuenta con Constancia de Situación Fiscal actualizada?' }}</p>
                        <v-row >
                          <v-col 
                          cols="12"
                          md="1"
                        >
                            <v-checkbox
                                label="Si"
                                  v-model="enabled"
                                  class="shrink mr-2 mt-0"
                                  
                              ></v-checkbox>
                            </v-col>
                            <v-col 
                          cols="12"
                          md="4"
                        >
                          <v-file-input
                              :disabled="!enabled"
                              label="Subir documento PDF"
                              outlined
                              filled  
                              dense
                              
                    ></v-file-input>
                            </v-col>
                       
                              <v-col 
                                cols="12"
                                md="3"
                              >
                                <v-checkbox
                                    v-model="checkbox"
                                    hide-details
                                    label="En trámite"
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>

                              <v-col 
                                cols="12"
                                md="3"
                              >
                                  <v-checkbox
                                    v-model="checkbox"
                                    label="No"
                                    hide-details
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>
                        </v-row>
                        
                </v-card-text>
>>>>>>> ef49abf8d926a0e1cb3c7b259d1248bac6fe5f17
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Tipo vialidad"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="5"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Nombre vialidad"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="2"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Num Ext"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="2"
                >
                  <v-text-field
                  hide-details
                    color="purple"
                    label="Num Int"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                  hide-details
                    color="purple"
                    label="Entre (vialidad)"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="5"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Nombre vialidad"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                  hide-details
                    color="purple"
                    label="Y (vialidad)"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="5"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Nombre vialidad"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Colonia (tipo)"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Colonia (nombre)"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Estado"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Municipio"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    hide-details
                    label="Ciudad"
                    filled
                  />
                </v-col>
                <v-card-text>
                  <p class="text-CENTER">{{ radios || '¿Cuenta con Constancia de Situación Fiscal actualizada?' }}</p>
                        <v-row>
                          <v-col
                          cols="12"
                          md="1"
                        >
                            <v-checkbox
                                label="Si"
                                  v-model="enabled"
                                  class="shrink mr-2 mt-0"
                              ></v-checkbox>
                            </v-col>
                            <v-col
                              cols="12"
                              md="4"
                            >
                          <v-file-input
                              :disabled="!enabled"
                              label="Subir documento PDF"
                              outlined
                              filled
                              dense
                    ></v-file-input>
                            </v-col>
                              <v-col
                                cols="12"
                                md="3"
                              >
                                <v-checkbox
                                    v-model="checkbox"
                                    hide-details
                                    label="En trámite"
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>

                              <v-col
                                cols="12"
                                md="3"
                              >
                                  <v-checkbox
                                    v-model="checkbox"
                                    label="No"
                                    hide-details
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>
                        </v-row>
                </v-card-text>
              </v-row>
        </v-tab-item>
   <!-- ------------------Persona moral------------------------- -->
        <v-tab-item>
         <v-row>
          <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    label="Denominación o razón social"
                    filled
                  />
                </v-col>

                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    label="RFC Persona moral"
                    filled
                  />
                </v-col>

                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    label="Correo electrónico fiscal"
                    filled
                  />
                </v-col>
                <v-card-text>
                  <p class="text-CENTER">{{ radios || '¿Cuenta con Constancia de Situación Fiscal actualizada?' }}</p>
                        <v-row>
                          <v-col
                          cols="12"
                          md="1"
                        >
                            <v-checkbox
                                label="Si"
                                  v-model="enabled"
                                  class="shrink mr-2 mt-0"
                              ></v-checkbox>
                            </v-col>
                            <v-col
                              cols="12"
                              md="4"
                            >
                          <v-file-input
                              :disabled="!enabled"
                              label="Subir documento PDF"
                              outlined
                              filled
                              dense
                    ></v-file-input>
                            </v-col>
                              <v-col
                                cols="12"
                                md="3"
                              >
                                <v-checkbox
                                    v-model="checkbox"
                                    hide-details
                                    label="En trámite"
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>
                              <v-col
                                cols="12"
                                md="3"
                              >
                                  <v-checkbox
                                    v-model="checkbox"
                                    label="No"
                                    hide-details
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>
                        </v-row>
                </v-card-text>
         </v-row>
        </v-tab-item>
      </v-tabs-items>
          <v-btn
            color="primary"
            @click="e1 = 3"
          >
            Continue
          </v-btn>
            <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
          <v-btn
            @click="e1 = 1"
            >
            Atras
          </v-btn>
        </v-stepper-content>
        <v-stepper-content step="3">
          <v-row>
            <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    label="Tipo"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    label="Nombre del establecimiento"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
                    label="RFC"
                    filled
                  />
                </v-col>
                <v-card-text>
                <p class="text-CENTER">{{ radios || '¿Cuenta con logotipo original y propio?' }}</p>
                        <v-row>
                          <v-col
                          cols="12"
                          md="1"
                        >
                            <v-checkbox
                                label="Si"
                                  v-model="enabled"
                                  class="shrink mr-2 mt-0"
                              ></v-checkbox>
                            </v-col>
                            <v-col
                          cols="12"
                          md="6"
                          >
                          <v-file-input
                              :disabled="!enabled"
                              label="Subir documento PDF"
                              outlined
                              filled
                              dense
                    ></v-file-input>
                            </v-col>
                            <v-col
                                cols="12"
                                md="2"
                              >
                                <v-checkbox
                                    v-model="checkbox"
                                    hide-details
                                    label="En proceso "
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>
                              <v-col
                                cols="12"
                                md="2"
                              >
                                  <v-checkbox
                                    v-model="checkbox"
                                    label="No"
                                    hide-details
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>
                            </v-row>
                          </v-card-text>
                          <v-col
                  cols="12"
                  md="4"
                >
                <p class="text-left">{{ radios || '¿Ha sido notificado por COFEPRIS?' }}</p>
                <v-radio-group
                    v-model="row"
                    row
                  >
                    <v-radio
                      label="Si"
                      value="radio-1"
                    ></v-radio>
                    <v-radio
                      label="No"
                      value="radio-2"
                    ></v-radio>
                  </v-radio-group>
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                <p class="text-left">{{ radios || '¿Cuenta con aviso de funcionamiento?' }}</p>
                <v-radio-group
                    v-model="row"
                    row
                  >
                    <v-radio
                      label="Si"
                      value="radio-1"
                    ></v-radio>
                    <v-radio
                      label="No"
                      value="radio-2"
                    ></v-radio>
                  </v-radio-group>
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                <p class="text-left">{{ radios || '¿Cuenta con cédula profesional?' }}</p>
                <v-radio-group
                    v-model="row"
                    row
                  >
                    <v-radio
                      label="Si"
                      @click="expand = !expand"
                    ></v-radio>

                    <v-radio
                      label="No"
                      @click="isdeleted"
                    ></v-radio>

                    <v-radio
                      label="En trámite"
                    ></v-radio>
                  </v-radio-group>
                </v-col>
                <v-col
                  cols="12"
                  md="5"
                >
                <p class="text-left">{{ radios || '¿Cuenta con redes sociales comerciales?' }}</p>
                <v-radio-group
                    v-model="row"
                    row
                  >
                    <v-radio
                      label="Si"
                      @click="expandi = !expandi"
                    ></v-radio>
                    <v-radio
                      label="No"
                    ></v-radio>
                  </v-radio-group>
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                <p class="text-left">{{ radios || '¿Cuenta con sitio web propio?' }}</p>
                <v-radio-group
                    v-model="row"
                    row
                  >
                    <v-radio
                      label="Si"
                      @click="expande = !expande"
                    ></v-radio>

                    <v-radio
                      label="No"
                    ></v-radio>
                  </v-radio-group>
                </v-col>
                <v-col
                    cols="12"
                    md="3"
                  ></v-col>
                <v-col
                    cols="12"
                    md="2"
                  >
                    <v-checkbox
                    v-show="expandi"
                        v-model="checkbox"
                        hide-details
                        label="Facebook "
                        class="shrink mr-2 mt-0"
                      ></v-checkbox>
                  </v-col>
                  <v-col
                    cols="12"
                    md="3"
                  >
                    <v-checkbox
                    v-show="expandi"
                        v-model="checkbox"
                        hide-details
                        label="Instagram "
                        class="shrink mr-2 mt-0"
                      ></v-checkbox>
                  </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                <v-text-field
                v-show="expande"
                    label="Sitio Web"
                    outlined
                    dense
                    filled
                  ></v-text-field></v-col>
          </v-row>
          <v-btn
            color="primary"
            @click="e1 = 4"
          >
            Continue
          </v-btn>
          <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
          <v-btn
            @click="e1 = 2"
            >
            Atras
          </v-btn>
        </v-stepper-content>
        <v-stepper-content step="4">

          <p class="text-left">Observaciones</p>
            <v-textarea
              v-model="title"
              label="Aquí puede escribir cualquier observación sobre los datos que ha introducido."
              full-width
              filled
            ></v-textarea>
            <v-col
              cols="12"
              md="12"
            >
            <v-form
            ref="form"
      v-model="valid"
      lazy-validation
      >
      <v-switch
      v-model="name"
        :rules="nameRules"
        required
        :label="`Estoy de acuerdo con que esta información será tratada con plena confidencialidad por parte de Guía Salud.`"
      ></v-switch>
            </v-form>
            </v-col>
<v-btn
  color="primary"
>
  Finalizar
</v-btn>
<v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
              <v-divider
              vertical
              ></v-divider>
<v-btn
  @click="e1 = 1"
  >
  Atras
</v-btn>
</v-stepper-content>
      </v-stepper-items>
    </v-stepper>
                </v-col>
              </v-row>
            </v-container>
          </v-form>
        </material-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
  export default {
    data () {
      return {
        tabs: null,
        e1: 1,
        expand: false,
        includeFiles: true,
        enabled: false,
        vue: {
          exp: null,
        },
      }
    },
  }
</script>
