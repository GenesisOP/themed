<template>
  <v-container
    id="user-profile-view"
    fluid
    tag="section"
  >
    <v-row justify="center">
      <v-col
        cols="12"
        md="8"
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
          Name of step 2
        </v-stepper-step>
  
        <v-divider></v-divider>
  
        <v-stepper-step step="3">
          Name of step 3
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
                  />
                </v-col>

                <v-col
                  cols="12"
                  md="3"
                >
                  <v-text-field
                    color="purple"
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
                    label="Telefono"
                    filled
                  />
                </v-col>

                <v-col cols="12"
                  md="8">
                  <v-text-field
                    color="purple"
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
  
          <v-btn text>
            Cancel
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
            <br></br>
              <v-col
                  cols="12"
                  md="6"
                >
                  <v-text-field
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
                    label="Nombre materno"
                    filled
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="4"
                >
                  <v-text-field
                    color="purple"
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
                    label="Correo electrónico fiscal"
                    filled
                  />
                </v-col>
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
                        <v-row align="center">
                            <v-checkbox
                                label="Si"
                                  v-model="enabled"
                                  class="shrink mr-2 mt-0"
                              ></v-checkbox>
                          <v-file-input
                              :disabled="!enabled"
                              label="File input"
                              outlined
                              filled  
                              dense
                    ></v-file-input>
                       
                              <v-col 
                                cols="12"
                                md="4"
                              >
                                <v-checkbox
                                    v-model="checkbox"
                                    label="En trámite"
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>

                              <v-col 
                                cols="12"
                                md="4"
                              >
                                  <v-checkbox
                                    v-model="checkbox"
                                    label="No"
                                    class="shrink mr-2 mt-0"
                                  ></v-checkbox>
                              </v-col>
                        </v-row>
                      
                </v-card-text>
                
              </v-row>
        </v-tab-item>
        <v-tab-item>
          <v-card flat>
              <p>
                Maecenas ullamcorper, dui et placerat feugiat, eros pede varius nisi, condimentum viverra felis nunc et lorem. Sed hendrerit. Maecenas malesuada. Vestibulum ullamcorper mauris at ligula. Proin faucibus arcu quis ante.
              </p>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
      
          <v-btn
            color="primary"
            @click="e1 = 3"
          >
            Continue
          </v-btn>
  
          <v-btn
            @click="e1 = 1">
            Atras
          </v-btn>
        </v-stepper-content>
  
        <v-stepper-content step="3">
          <v-card
            class="mb-12"
            color="grey lighten-1"
            height="200px"
          ></v-card>
  
          <v-btn
            color="primary"
            @click="e1 = 1"
          >
            Continue
          </v-btn>
  
          <v-btn
            @click="e1 = 2">
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

      <v-col
        cols="12"
        md="2"
      >
        <app-card class="mt-4 text-center">
          <v-img
            class="rounded-circle elevation-6 mt-n12 d-inline-block"
            src="https://demos.creative-tim.com/vue-material-dashboard/img/marc.aba54d65.jpg"
            width="128"
          />

          <v-card-text class="text-center">
            <h6 class="text-h6 mb-2 text--secondary">
              CEO / FOUNDER
            </h6>

            <h4 class="text-h4 mb-3 text--primary">
              John Leider
            </h4>

            <p class="text--secondary">
              Lorem ipsum dolor, sit amet consectetur adipisicing elit. Ratione dolorem deserunt veniam tempora magnam quisquam quam error iusto cupiditate ducimus
            </p>

            <v-btn
              class="mr-0"
              color="primary"
              min-width="100"
              rounded
            >
              Folssslow
            </v-btn>
          </v-card-text>
        </app-card>
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
         
        }
      }
    },
  }
</script>
