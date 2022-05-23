<script>
import data from "./components/Data.json";

export default {
  data() {
    return {
      data: data,
      selectedDzimums: "",
      selectedVecums: "",
      dzimums: [{ value: "sieviete" }, { value: "vīrietis" }],
      vecums: [
        { value: "18-24" },
        { value: "25-34" },
        { value: "35-44" },
        { value: "45-54" },
        { value: "55+" },
      ],
      rezultati: "",
      modal: false,
    };
  },
  methods: {
    rezultatuAprekins(vecums, dzimums) {
      if (vecums !== "" && dzimums !== "") {
        var vertiba = String(
          dzimums + "_" + vecums.replace("-", "_").replace("+", "")
        );
        this.rezultati = this.data[vertiba].balss;
        this.modal = true;
      }
    },
    aizvert() {
      this.modal = false;
    },
  },
};
</script>

<template>
  <div id="header"></div>
  <div id="lietotne">
    <h1>Piemērotākās balss noteicējs</h1>
    <p class="info">
      Atzīmē demogrāfiskos datus un spied "Aprēķināt rezultātus"
    </p>
    <div>
      <select v-model="selectedVecums">
        <option disabled value="">Mērķauditorijas vecums</option>
        <option v-for="v in vecums" v-bind:key="v.value">{{ v.value }}</option>
      </select>
    </div>
    <div>
      <select v-model="selectedDzimums">
        <option disabled value="">Mērķauditorijas dzimums</option>
        <option v-for="d in dzimums" v-bind:key="d.value">{{ d.value }}</option>
      </select>
    </div>
    <div>
      <br />
      <button @click="rezultatuAprekins(selectedVecums, selectedDzimums)">
        Aprēķināt rezultātus
      </button>
      <div id="modal" v-if="modal === true">
        <p id="rezultati">
          Ieteicamā balss mērķauditorijai {{ selectedDzimums }}
          {{ selectedVecums }} ir: <br />
          <br />
          <span id="rezultatiSvarigie"> {{ rezultati }} balss </span>
          <button id="aizvertPoga" @click="aizvert()">Aizvērt</button>
        </p>
      </div>
      <p class="infoApaksa">
        *Vidējā frekvence sievietēm ir 233 Hz, vīriešiem 16 Hz. Augsta - pustoni
        augstāk, zema - pustoni zemāk
      </p>
    </div>
    <img src="./assets/pic_from_google.jpg" />
  </div>
</template>

<style scoped>
#lietotne {
  margin-top: 10%;
  margin-left: 10%;
}
#header {
  background-color: firebrick;
  height: 10px;
  padding: 0;
}
img {
  max-width: 60%;
  position: absolute;
  top: 40%;
  right: 0px;
  z-index: -999;
}
.info {
  font-size: 12px;
  margin-bottom: 5%;
  color: dimgray;
}
.infoApaksa {
  font-size: 12px;
  margin-bottom: 5%;
  color: dimgray;
  width: 40%;
}
#modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}
#rezultati {
  text-align: center;
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 50%;
  font-size: 16px;
  margin-left: 25%;
  box-shadow: 5px 10px 8px 10px #888888;
  color: dimgray;
}
#aizvertPoga {
  display: block;
  text-align: center;
  font-size: 14px;
  margin-left: 35%;
  margin-top: 10%;
  padding: 15px;
}
#rezultatiSvarigie {
  font-size: 26px;
  color: black;
}
select {
  position: relative;
  height: 36px;
  width: 50%;
  margin-top: 14px;
  margin-bottom: 14px;
  background-color: #fff;
  border-radius: 4px;
  cursor: pointer;
}
h1 {
  margin-bottom: 0px;
  font-weight: normal;
  font-size: 40px;
  font-weight: normal;
  text-transform: uppercase;
  color: #fa6400;
}

button {
  align-items: center;
  background-clip: padding-box;
  background-color: #fa6400;
  border: 1px solid transparent;
  border-radius: 0.25rem;
  box-shadow: rgba(0, 0, 0, 0.02) 0 1px 3px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  display: inline-flex;
  font-family: system-ui, -apple-system, system-ui, "Helvetica Neue", Helvetica,
    Arial, sans-serif;
  font-size: 16px;
  font-weight: 600;
  justify-content: center;
  line-height: 1.25;
  margin: 0;
  min-height: 3rem;
  padding: calc(0.875rem - 1px) calc(1.5rem - 1px);
  position: relative;
  text-decoration: none;
  transition: all 250ms;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: baseline;
  width: auto;
}
</style>