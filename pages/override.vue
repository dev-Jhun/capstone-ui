<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-card color="#CDE8E5" elevation="2" class="switch-card" light>
          <!-- Switch to toggle mode -->
          <v-switch
            v-model="autoMode"
            label="AUTOMATIC MODE"
            @change="updateMode"
            class="switch-large"
            style="color: white; font-weight: bold"
          />
        </v-card>
      </v-col>

      <v-col cols="12" md="4" sm="6">
        <v-card color="#F2F597" class="pa-4">
          <v-card-title class="d-flex justify-center">
            TEMPERATURE MISTING
          </v-card-title>
          <v-list-item two-line class="d-flex justify-center align-center">
            <v-list-item-content>
              <v-list-item-subtitle>AIR TEMPERATURE</v-list-item-subtitle>
              <v-divider></v-divider>
              <v-list-item-title class="display-2">{{
                latestTemp
              }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>

          <v-row justify="center" align="center">
            <v-col cols="auto">
              <v-btn
                color="green"
                dark
                @click="turnOnMistingTemp"
                :disabled="isButtonDisabled"
              >
                <template v-if="!isMistingRunningTemp"> On </template>
                <template v-else>
                  <v-progress-circular
                    indeterminate
                    color="white"
                    size="20"
                    width="2"
                  ></v-progress-circular>
                </template>
              </v-btn>
            </v-col>
            <v-col cols="auto">
              <v-btn
                color="red"
                dark
                @click="turnOffMistingTemp"
                :disabled="autoMode"
              >
                Off
              </v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col cols="12" md="4" sm="6">
        <v-card color="#AAD9BB" class="pa-4">
          <v-card-title class="d-flex justify-center">
            HUMIDITY MISTING
          </v-card-title>
          <v-list-item two-line class="d-flex justify-center align-center">
            <v-list-item-content>
              <v-list-item-subtitle>HUMIDITY</v-list-item-subtitle>
              <v-divider></v-divider>
              <v-list-item-title class="display-2">{{
                latestHumid
              }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-row justify="center" align="center">
            <v-col cols="auto">
              <v-btn
                color="green"
                dark
                @click="turnOnMistingHumid"
                :disabled="isButtonDisabled"
              >
                <template v-if="!isMistingRunningHumid"> On </template>
                <template v-else>
                  <v-progress-circular
                    indeterminate
                    color="white"
                    size="20"
                    width="2"
                  ></v-progress-circular>
                </template>
              </v-btn>
            </v-col>
            <v-col cols="auto">
              <v-btn
                color="red"
                dark
                @click="turnOffMistingHumid"
                :disabled="autoMode"
              >
                Off
              </v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col cols="12" md="4" sm="6">
        <v-card color="#86B6F6" class="pa-4">
          <v-card-title class="d-flex justify-center"> PH PUMPS </v-card-title>
          <v-list-item two-line class="d-flex justify-center align-center">
            <v-list-item-content>
              <v-list-item-subtitle>PH LEVEL</v-list-item-subtitle>
              <v-divider></v-divider>
              <v-list-item-title class="display-2">{{
                latestPh
              }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-row justify="center" align="center">
            <v-col cols="auto">
              <v-btn
                color="green"
                dark
                @click="turnOnPhUpPump"
                :disabled="isButtonDisabled"
              >
                <template v-if="!isPhPumpUpRunning">+ ON</template>
                <template v-else>
                  <v-progress-circular
                    indeterminate
                    color="white"
                    size="20"
                    width="2"
                  ></v-progress-circular>
                </template>
              </v-btn>
              <v-btn
                color="red"
                dark
                @click="turnOffPhUpPump"
                :disabled="isButtonDisabled"
                >+ OFF
              </v-btn>
            </v-col>
            <v-col cols="auto">
              <v-btn
                color="green"
                dark
                @click="turnOnPhDownPump"
                :disabled="autoMode"
              >
                <template v-if="!isPhPumpDownRunning">- ON</template>
                <template v-else>
                  <v-progress-circular
                    indeterminate
                    color="white"
                    size="20"
                    width="2"
                  ></v-progress-circular>
                </template>
              </v-btn>
              <v-btn
                color="red"
                dark
                @click="turnOffPhDownPump"
                :disabled="autoMode"
                >- OFF
              </v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col cols="12" md="4" sm="6">
        <v-card color="#F3CCF3" class="pa-4">
          <v-card-title class="d-flex justify-center"> TDS PUMPS </v-card-title>
          <v-list-item two-line class="d-flex justify-center align-center">
            <v-list-item-content>
              <v-list-item-subtitle>TDS LEVEL</v-list-item-subtitle>
              <v-divider></v-divider>
              <v-list-item-title class="display-2">{{
                latestTds
              }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-row justify="center" align="center">
            <v-col cols="auto">
              <v-btn
                color="green"
                dark
                @click="turnOnTdsAPump"
                :disabled="isButtonDisabled"
              >
                <template v-if="!isTdsPumpARunning">A ON</template>
                <template v-else>
                  <v-progress-circular
                    indeterminate
                    color="white"
                    size="20"
                    width="2"
                  ></v-progress-circular>
                </template>
              </v-btn>
              <v-btn
                color="red"
                dark
                @click="turnOffTdsAPump"
                :disabled="isButtonDisabled"
                >A OFF
              </v-btn>
            </v-col>
            <v-col cols="auto">
              <v-btn
                color="green"
                dark
                @click="turnOnTdsBPump"
                :disabled="autoMode"
              >
                <template v-if="!isTdsPumpBRunning">B ON</template>
                <template v-else>
                  <v-progress-circular
                    indeterminate
                    color="white"
                    size="20"
                    width="2"
                  ></v-progress-circular>
                </template>
              </v-btn>
              <v-btn
                color="red"
                dark
                @click="turnOffTdsBPump"
                :disabled="autoMode"
                >B OFF
              </v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col cols="12" md="4" sm="6">
        <v-card color="#FDE49E" class="pa-4">
          <v-card-title class="d-flex justify-center">
            WATER PUMP
          </v-card-title>
          <v-list-item two-line class="d-flex justify-center align-center">
            <v-list-item-content>
              <v-list-item-subtitle>WATER TEMPERATURE</v-list-item-subtitle>
              <v-divider></v-divider>
              <v-list-item-title class="display-2">{{
                latestWaterTemp
              }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>

          <v-row justify="center" align="center">
            <v-col cols="auto">
              <v-btn
                color="green"
                dark
                @click="turnOnTdsWaterPump"
                :disabled="isButtonDisabled"
              >
                <template v-if="!isTdsWaterPumpRunning"> On </template>
                <template v-else>
                  <v-progress-circular
                    indeterminate
                    color="white"
                    size="20"
                    width="2"
                  ></v-progress-circular>
                </template>
              </v-btn>
            </v-col>
            <v-col cols="auto">
              <v-btn
                color="red"
                dark
                @click="turnOffTdsWaterPump"
                :disabled="autoMode"
              >
                Off
              </v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>

    <!-- Snackbar for success message -->
    <v-snackbar
      v-model="successSnackbar"
      color="green"
      bottom
      :timeout="snackbarTimeout"
    >
      {{ successMessage }}
      <template v-slot:action="{ attrs }">
        <v-btn
          color="white"
          text
          v-bind="attrs"
          @click="successSnackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>

    <!-- Snackbar for error message -->
    <v-snackbar
      v-model="errorSnackbar"
      color="red"
      bottom
      :timeout="snackbarTimeout"
    >
      {{ errorMessage }}
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
      autoMode: false, // Default to manual mode
      buttonLabel: "START MISTING", // Initial button label
      snackbarTimeout: 5000, // Duration for the snackbar to remain visible (in milliseconds)

      // Snackbar properties
      successSnackbar: false,
      errorSnackbar: false,
      successMessage: "",
      errorMessage: "",

      //sensor valuess
      latestTemp: "0",
      latestHumid: "0",
      latestPh: "0",
      latestTds: "0",
      latestWaterTemp: "0",

      isMistingRunningTemp: false, // Flag to indicate if misting is running
      isMistingRunningHumid: false, // Flag to indicate if misting is running

      isPhPumpUpRunning: false, // Flag to indicate if phup is running
      isPhPumpDownRunning: false, // Flag to indicate if phup is running

      isTdsPumpARunning: false, // Flag to indicate if solution a is running
      isTdsPumpBRunning: false, // Flag to indicate if solution b is running
      isTdsWaterPumpRunning: false, // Flag to indicate if solution b is running
    };
  },

  //   mounted() {
  //     // Fetch the initial mode value from Firebase when the component is mounted
  //     firebase
  //       .database()
  //       .ref("mode/auto")
  //       .once("value", (snapshot) => {
  //         const modeValue = snapshot.val();
  //         if (modeValue !== null) {
  //           this.autoMode = modeValue === "1";
  //         }
  //       });
  //   },

  methods: {
    updateMode() {
      // Update mode value in Firebase
      firebase
        .database()
        .ref("mode/auto")
        .set(this.autoMode ? "1" : "0")
        .then(() => {
          // If mode update is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Mode updated successfully";

          // If mode is switched to manual (mode 0), turn off all pumps
          if (!this.autoMode) {
            this.successSnackbar = true;
            this.successMessage = "All pumps stopped!";
            this.turnOffAllPumps();
            
          }
        })
        .catch((error) => {
          // If an error occurs during mode update, show error snackbar
          console.error("Error updating mode:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error updating mode";
        });
    },

    turnOffAllPumps() {
      // Turn off all pumps by calling each turn off method
      this.turnOffMistingTemp();
      this.turnOffMistingHumid();
      this.turnOffPhUpPump();
      this.turnOffPhDownPump();
      this.turnOffTdsAPump();
      this.turnOffTdsBPump();
    },

    //temperature misting
    turnOnMistingTemp() {
      this.isMistingRunningTemp = true;
      // Send value 1 to Firebase database
      firebase
        .database()
        .ref("temp/tempmist")
        .set("1")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Misting is running successfully!";
          // setTimeout(() => {
          //   this.isMistingRunningTemp = false; // Reset flag
          // }, 10000 * 6);
          // // Set a timeout to revert the value back to 0 after 60 seconds
          // setTimeout(() => {
          //   firebase.database().ref("temp/tempmist").set(0);
          // }, 10000 * 6);
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error sending value to Firebase:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Misting running failed!";
        });
    },

    turnOffMistingTemp() {
      // Change button label to indicate that misting is stopped
      this.isMistingRunningTemp = false;
      // Send value 0 to Firebase database to turn off misting
      firebase
        .database()
        .ref("temp/tempmist")
        .set("0")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Misting stopped!";
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error turning off misting:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error stopping misting!";
        });
    },

    // humid
    turnOnMistingHumid() {
      this.isMistingRunningHumid = true;
      // Send value 1 to Firebase database
      firebase
        .database()
        .ref("humid/humidmist")
        .set("1")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Misting is running successfully!";
          // setTimeout(() => {
          //   this.isMistingRunningHumid = false; // Reset flag
          // }, 10000 * 6);
          // // Set a timeout to revert the value back to 0 after 60 seconds
          // setTimeout(() => {
          //   firebase.database().ref("humid/humidmist").set(0);
          // }, 10000 * 6);
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error sending value to Firebase:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Misting running failed!";
        });
    },

    turnOffMistingHumid() {
      // Change button label to indicate that misting is stopped
      this.isMistingRunningHumid = false;
      // Send value 0 to Firebase database to turn off misting
      firebase
        .database()
        .ref("humid/humidmist")
        .set("0")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Misting stopped!";
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error turning off misting:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error stopping misting!";
        });
    },

    // ph
    turnOnPhUpPump() {
      this.isPhPumpUpRunning = true;
      // Send value 1 to Firebase database
      firebase
        .database()
        .ref("ph/pHpumpHigh")
        .set("1")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "PH UP pump is running successfully!";
          //   setTimeout(() => {
          //     this.isPhPumpUpRunning = false; // Reset flag
          //   }, 10000);
          //   // Set a timeout to revert the value back to 0 after 60 seconds
          //   setTimeout(() => {
          //     firebase.database().ref("ph/pHpumpHigh").set(0);
          //   }, 10000);
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error sending value to Firebase:", error);
          this.errorSnackbar = true;
          this.errorMessage = "PH UP pump running failed!";
        });
    },

    turnOffPhUpPump() {
      // Change button label to indicate that misting is stopped
      this.isPhPumpUpRunning = false;
      // Send value 0 to Firebase database to turn off misting
      firebase
        .database()
        .ref("ph/pHpumpHigh")
        .set("0")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Ph UP Pump stopped!";
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error turning off ph up pump:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error stopping ph up pump!";
        });
    },

    turnOnPhDownPump() {
      this.isPhPumpDownRunning = true;
      // Send value 1 to Firebase database
      firebase
        .database()
        .ref("ph/pHpumpLow")
        .set("1")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "PH Down pump is running successfully!";
          //   setTimeout(() => {
          //     this.isPhPumpDownRunning = false; // Reset flag
          //   }, 10000);
          //   // Set a timeout to revert the value back to 0 after 60 seconds
          //   setTimeout(() => {
          //     firebase.database().ref("ph/pHpumpLow").set(0);
          //   }, 10000);
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error sending value to Firebase:", error);
          this.errorSnackbar = true;
          this.errorMessage = "PH Down pump running failed!";
        });
    },

    turnOffPhDownPump() {
      // Change button label to indicate that misting is stopped
      this.isPhPumpDownRunning = false;
      // Send value 0 to Firebase database to turn off ph down
      firebase
        .database()
        .ref("ph/pHpumpLow")
        .set("0")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Ph DOWN Pump stopped!";
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error turning off ph down pump:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error stopping ph down pump!";
        });
    },

    // tds
    turnOnTdsAPump() {
      this.isTdsPumpARunning = true;
      // Send value 1 to Firebase database
      firebase
        .database()
        .ref("tds/tdspumpA")
        .set("1")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "SOLUTION A pump is running successfully!";
          //   setTimeout(() => {
          //     this.isPhPumpUpRunning = false; // Reset flag
          //   }, 10000);
          //   // Set a timeout to revert the value back to 0 after 60 seconds
          //   setTimeout(() => {
          //     firebase.database().ref("ph/pHpumpHigh").set(0);
          //   }, 10000);
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error sending value to Firebase:", error);
          this.errorSnackbar = true;
          this.errorMessage = "SOLUTION A pump running failed!";
        });
    },

    turnOffTdsAPump() {
      // Change button label to indicate that misting is stopped
      this.isTdsPumpARunning = false;
      // Send value 0 to Firebase database to turn off misting
      firebase
        .database()
        .ref("tds/tdspumpA")
        .set("0")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "SOLUTION A Pump stopped!";
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error turning off ph up pump:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error stopping solution A pump!";
        });
    },

    turnOnTdsBPump() {
      this.isTdsPumpBRunning = true;
      // Send value 1 to Firebase database
      firebase
        .database()
        .ref("tds/tdspumpB")
        .set("1")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Solution B pump is running successfully!";
          //   setTimeout(() => {
          //     this.isPhPumpDownRunning = false; // Reset flag
          //   }, 10000);
          //   // Set a timeout to revert the value back to 0 after 60 seconds
          //   setTimeout(() => {
          //     firebase.database().ref("ph/pHpumpLow").set(0);
          //   }, 10000);
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error sending value to Firebase:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Solution B pump running failed!";
        });
    },

    turnOffTdsBPump() {
      // Change button label to indicate that misting is stopped
      this.isTdsPumpBRunning = false;
      // Send value 0 to Firebase database to turn off ph down
      firebase
        .database()
        .ref("tds/tdspumpB")
        .set("0")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Solution B Pump stopped!";
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error turning off solution b pump:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error stopping solution b pump!";
        });
    },


    turnOnTdsWaterPump() {
      this.isTdsWaterPumpRunning = true;
      // Send value 1 to Firebase database
      firebase
        .database()
        .ref("tds/tdswaterpump")
        .set("1")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Water pump runs successfully!";
          //   setTimeout(() => {
          //     this.isPhPumpDownRunning = false; // Reset flag
          //   }, 10000);
          //   // Set a timeout to revert the value back to 0 after 60 seconds
          //   setTimeout(() => {
          //     firebase.database().ref("ph/pHpumpLow").set(0);
          //   }, 10000);
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error sending value to Firebase:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Water pump runs failed!";
        });
    },

    turnOffTdsWaterPump() {
      // Change button label to indicate that misting is stopped
      this.isTdsWaterPumpRunning = false;
      // Send value 0 to Firebase database to turn off ph down
      firebase
        .database()
        .ref("tds/tdswaterpump")
        .set("0")
        .then(() => {
          // If sending value is successful, show success snackbar
          this.successSnackbar = true;
          this.successMessage = "Waterpump stopped!";
        })
        .catch((error) => {
          // If an error occurs, show error snackbar
          console.error("Error turning off solution b pump:", error);
          this.errorSnackbar = true;
          this.errorMessage = "Error stopping waterpump!";
        });
    },


    //to fetch temperature latest data
    async fetchLatestTemp() {
      try {
        const tempRef = firebase.database().ref("temp");
        const snapshot = await tempRef.once("value");
        const data = snapshot.val();
        if (data && data.tempcurrent !== undefined) {
          this.latestTemp = data.tempcurrent;
        }
      } catch (error) {
        console.error("Error fetching latest temperature data:", error);
      }
    },

    //to fetch humid latest data
    async fetchLatestHumid() {
      try {
        const humidRef = firebase.database().ref("humid");
        const snapshot = await humidRef.once("value");
        const data = snapshot.val();
        if (data && data.humidcurrent !== undefined) {
          this.latestHumid = data.humidcurrent;
        }
      } catch (error) {
        console.error("Error fetching latest Humid data:", error);
      }
    },

    async fetchLatestPh() {
      try {
        const PhRef = firebase.database().ref("ph");
        const snapshot = await PhRef.once("value");
        const data = snapshot.val();
        if (data && data.pHcurrent !== undefined) {
          this.latestPh = parseFloat(data.pHcurrent.toFixed(1));
        }
      } catch (error) {
        console.error("Error fetching latest Ph data:", error);
      }
    },

    //to fetch tds latest data
    async fetchLatestTds() {
      try {
        const tdsRef = firebase.database().ref("tds");
        const snapshot = await tdsRef.once("value");
        const data = snapshot.val();
        if (data && data.tdscurrent !== undefined) {
          this.latestTds = parseFloat(data.tdscurrent.toFixed(1));
        }
      } catch (error) {
        console.error("Error fetching latest Tds data:", error);
      }
    },
    //to fetch water temp latest data
    async fetchLatestWaterTemp() {
      try {
        const waterTempRef = firebase.database().ref("watertemp");
        const snapshot = await waterTempRef.once("value");
        const data = snapshot.val();
        if (data && data.watercurrent !== undefined) {
          this.latestWaterTemp = parseFloat(data.watercurrent.toFixed(1));
        }
      } catch (error) {
        console.error("Error fetching latest water temp data:", error);
      }
    },
  },

  mounted() {
    firebase
      .database()
      .ref("mode/auto")
      .once("value", (snapshot) => {
        const modeValue = snapshot.val();
        if (modeValue !== null) {
          this.autoMode = modeValue === "1";
        }
      });

    // Call each fetch function every second
    setInterval(this.fetchLatestTemp, 1000);
    setInterval(this.fetchLatestHumid, 1000);
    setInterval(this.fetchLatestPh, 1000);
    setInterval(this.fetchLatestTds, 1000);
    setInterval(this.fetchLatestWaterTemp, 1000);
    // setInterval(this.fetchLatestCropName, 1000);
    // setInterval(this.fetchLatestCropVar, 1000);

    //reference values
  },

  computed: {
    isButtonDisabled() {
      return this.autoMode; // Return true if autoMode is true, false otherwise
    },
  },
};
</script>
  
  <style scoped>
.switch-large {
  font-weight: bold;
}

.switch-card {
  display: flex;
  justify-content: center;
}
</style>
  