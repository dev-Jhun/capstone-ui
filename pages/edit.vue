<template>
  <v-container>
    <v-form @submit.prevent="submitForm">
      <v-row>
        <v-col cols="12" sm="6">
          <v-text-field
            v-model="formData.cropName"
            label="CROP NAME"
            required
            outlined
            elevation="5"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="6">
          <v-text-field
            v-model="formData.cropVariation"
            label="CROP VARIATION"
            outlined
            elevation="5"
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="6">
          <v-card class="pa-4" outlined elevation="5">
            <v-card-title class="d-flex justify-center align-center"
              >TEMPERATURE</v-card-title
            >
            <v-row dense>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropTempMin"
                  label="MIN"
                  required
                  type="number"
                  min="1"
                  max="50"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropTempMax"
                  label="MAX"
                  required
                  type="number"
                  min="1"
                  max="50"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="formData.cropTempRef"
                  label="REFERENCE"
                  required
                  type="number"
                  min="1"
                  max="5"
                  outlined
                ></v-text-field>
              </v-col>
            </v-row>
          </v-card>
        </v-col>

        <v-col cols="12" sm="6">
          <v-card class="pa-4" outlined elevation="5">
            <v-card-title class="d-flex justify-center align-center"
              >HUMIDITY</v-card-title
            >
            <v-row dense>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropHumidMin"
                  label="MIN"
                  required
                  type="number"
                  min="1"
                  max="100"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropHumidMax"
                  label="MAX"
                  required
                  type="number"
                  min="1"
                  max="100"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="formData.cropHumidRef"
                  label="REFERENCE"
                  required
                  type="number"
                  min="1"
                  max="100"
                  outlined
                ></v-text-field>
              </v-col>
            </v-row>
          </v-card>
        </v-col>

        <v-col cols="12" sm="6">
          <v-card class="pa-4" outlined elevation="5">
            <v-card-title class="d-flex justify-center align-center"
              >PH LEVEL</v-card-title
            >
            <v-row dense>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropPhMin"
                  label="MIN"
                  required
                  type="number"
                  min="1"
                  max="14"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropPhMax"
                  label="MAX"
                  required
                  type="number"
                  min="1"
                  max="14"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="formData.cropPhRef"
                  label="REFERENCE"
                  required
                  type="number"
                  min="1"
                  max="14"
                  outlined
                ></v-text-field>
              </v-col>
            </v-row>
          </v-card>
        </v-col>

        <v-col cols="12" sm="6">
          <v-card class="pa-4" outlined elevation="5">
            <v-card-title class="d-flex justify-center align-center"
              >TDS LEVEL</v-card-title
            >
            <v-row dense>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropTdsMin"
                  label="MIN"
                  required
                  type="number"
                  min="1"
                  max="5000"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  v-model="formData.cropTdsMax"
                  label="MAX"
                  required
                  type="number"
                  min="1"
                  max="5000"
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="formData.cropTdsRef"
                  label="REFERENCE"
                  required
                  type="number"
                  min="1"
                  max="5000"
                  outlined
                ></v-text-field>
              </v-col>
            </v-row>
          </v-card>
        </v-col>

        <v-col cols="12" sm="6">
          <v-card class="pa-4" outlined elevation="5">
            <v-card-title class="d-flex justify-center align-center"
              >WATER TEMPERATURE</v-card-title
            >
            <v-row dense>
              <v-col cols="12">
                <v-text-field
                  v-model="formData.cropWaterTempRef"
                  label="REFERENCE"
                  required
                  type="number"
                  min="1"
                  max="50"
                  outlined
                ></v-text-field>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>

      <br />
      <br />

      <v-row>
        <v-spacer></v-spacer>
        <v-col>
          <v-spacer></v-spacer>
          <v-btn type="submit" color="green" dark large>UPDATE PRESET</v-btn>
          <v-btn to="/plant" color="red" dark large>CANCEL PRESET</v-btn>
        </v-col>
        <v-spacer></v-spacer>
      </v-row>
      <br />
      <br />
      <br />
    </v-form>

    <!-- SUCCESS SNACKBAR     -->
    <v-snackbar color="green" v-model="successSnackbar">
      {{ textSuccess }}
      <template v-slot:action="{ attrs }">
        <v-btn
          plain
          color="white"
          v-bind="attrs"
          @click="successSnackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>

    <!-- ERROR SNACKBAR     -->
    <v-snackbar color="red" v-model="errorSnackbar">
      {{ textError }}
      <template v-slot:action="{ attrs }">
        <v-btn color="white" text v-bind="attrs" @click="errorSnackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </v-container>
</template>
    
<script>
import firebase from "~/plugins/firebase";

export default {
  data() {
    return {
      formData: {

        cropName: "",
        cropVariation: "",

        cropTempMin: "",
        cropTempMax: "",
        cropTempRef: "",
        cropTempMist: 0,
        tempcurrent: 0,

        cropHumidMin: "",
        cropHumidMax: "",
        cropHumidRef: "",
        cropHumidMist: 0,
        humidcurrent: 0,


        cropPhMin: "",
        cropPhMax: "",
        cropPhRef: "",
        pumpPhHigh: 0,
        pumpPhLow: 0,
        pHcurrent: 0,

        cropTdsMin: "",
        cropTdsMax: "",
        cropTdsRef: "",
        cropTdsPumpA: 0,
        cropTdsPumpB: 0,
        tdscurrent: 0,


        cropWaterTempRef: "",
      },
      successSnackbar: false,
      errorSnackbar: false,
      textSuccess: "",
      textError: "",
    };
  },
  mounted() {
    const presetId = this.$route.query.id;
    if (presetId) {
      this.fetchPresetData(presetId);
    }
  },
  methods: {
    async fetchPresetData(presetId) {
      try {
        const snapshot = await firebase
          .database()
          .ref(`details/${presetId}`)
          .once("value");
        const presetData = snapshot.val();

        console.log("Retrieved preset data:", presetData);

        if (presetData) {
          this.formData = {

            cropName: this.trimQuotes(presetData.name),
            cropVariation: this.trimQuotes(presetData.variation),

            cropTempMin: this.trimQuotes(presetData.temperature?.min),
            cropTempMax: this.trimQuotes(presetData.temperature?.max),
            cropTempRef: this.trimQuotes(presetData.temperature?.ref),
            cropTempMist: this.trimQuotes(presetData.temperature?.tempmist),
            tempcurrent: this.trimQuotes(presetData.temperature?.tempcurrent),

            cropHumidMin: this.trimQuotes(presetData.humidity?.min),
            cropHumidMax: this.trimQuotes(presetData.humidity?.max),
            cropHumidRef: this.trimQuotes(presetData.humidity?.ref),
            cropHumidMist: this.trimQuotes(presetData.humidity?.humidmist),
            humidcurrent: this.trimQuotes(presetData.humidity?.humidcurrent),

            cropPhMin: this.trimQuotes(presetData.pH?.min),
            cropPhMax: this.trimQuotes(presetData.pH?.max),
            cropPhRef: this.trimQuotes(presetData.pH?.ref),
            pumpPhHigh: this.trimQuotes(presetData.pH?.pHpumpHigh),
            pumpPhLow: this.trimQuotes(presetData.pH?.pHpumpLow),
            pHcurrent: this.trimQuotes(presetData.pH?.pHcurrent),

            cropTdsMin: this.trimQuotes(presetData.tds?.min),
            cropTdsMax: this.trimQuotes(presetData.tds?.max),
            cropTdsRef: this.trimQuotes(presetData.tds?.ref),
            cropTdsPumpA: this.trimQuotes(presetData.tds?.tdspumpA),
            cropTdsPumpB: this.trimQuotes(presetData.tds?.tdspumpB),
            tdscurrent: this.trimQuotes(presetData.tds?.tdscurrent),

            cropWaterTempRef: this.trimQuotes(presetData.watertemp),
          };

          console.log("Form data:", this.formData);
        }
      } catch (error) {
        console.error("Error fetching preset data:", error);
      }
    },
    async submitForm() {
      try {
        const presetId = this.$route.query.id;
        const updatedData = {
          name: this.formData.cropName,
          variation: this.formData.cropVariation,
          watertemp: this.formData.cropWaterTempRef,
          temperature: {
            min: this.formData.cropTempMin,
            max: this.formData.cropTempMax,
            ref: this.formData.cropTempRef,
            tempmist: this.formData.cropTempMist,
            tempcurrent: this.formData.tempcurrent,
          },
          humidity: {
            min: this.formData.cropHumidMin,
            max: this.formData.cropHumidMax,
            ref: this.formData.cropHumidRef,
            humidmist: this.formData.cropHumidMist,
            humidcurrent: this.formData.humidcurrent,
          },
          pH: {
            min: this.formData.cropPhMin,
            max: this.formData.cropPhMax,
            ref: this.formData.cropPhRef,
            pHpumpHigh: this.formData.pumpPhHigh,
            pHpumpLow: this.formData.pumpPhLow,
            pHcurrent: this.formData.pHcurrent,
          },
          tds: {
            min: this.formData.cropTdsMin,
            max: this.formData.cropTdsMax,
            ref: this.formData.cropTdsRef,
            tdspumpA: this.formData.cropTdsPumpA,
            tdspumpB: this.formData.cropTdsPumpB,
            tdscurrent: this.formData.tdscurrent,
          },
        };

        await firebase
          .database()
          .ref(`details/${presetId}`)
          .update(updatedData);

        console.log("Data updated successfully!");
        this.successSnackbar = true;
        this.textSuccess = "Presets Successfully Updated!";

        setTimeout(() => {
          this.$router.push("/plant");
        }, 2000);
      } catch (error) {
        console.error("Error updating data: ", error);
        this.errorSnackbar = true;
        this.textError = "Failed to update presets!";
      }
    },
    trimQuotes(value) {
      if (typeof value === 'string' || value instanceof String) {
        return value.replace(/^"|"$/g, '');
      } else if (value === undefined) {
        return '';
      }
      return value;
    },
  },
};
</script>


  