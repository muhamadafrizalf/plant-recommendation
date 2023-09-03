<template>
  <div class="home">
    <div v-if="!submitted">
      <h1>Aplikasi untuk memberikan rekomendasi tanaman berdasarkan kondisi wilayah</h1>
      <form @submit.prevent="submitForm">
        <label>Suhu dalam derajat Celius</label>
        <input v-model="temperature" type="number" required step=".1">
        <label>Kelembaban relatif dalam %</label>
        <input v-model="humidity" type="number" required step="0" min="0" max="100">
        <label>Nilai pH tanah</label>
        <input v-model="ph" type="number" required step=".1" min="0" max="14">
        <label>Curah hujan dalam mm</label>
        <input v-model="rainfall" type="number" required step="0" min="0">
        <div class="submit">
          <button>Cek rekomendasi tanaman</button>
        </div>
      </form>
    </div>
    <div v-else>
      <div class="result">
        <h1>Rekomendasi Tanaman</h1>
        <h2>{{ recommend.name }}</h2>
        <img :src="recommend.img" alt="recommend.name">
        <p>
          Tanaman yang cocok ditanam di wilayah yang memiliki suhu {{ temperature }}°C,
          kelembaban relatif {{ humidity }}%, nilai pH tanah {{ ph }}, dan memiliki curah
          hujan {{ rainfall }}mm adalah tanaman {{ recommend.name }}.
        </p>
        <button @click="isSubmitted" v-show="submitted">Kembali</button>
      </div>
    </div>
  </div>
</template>

<script>
import * as tf from '@tensorflow/tfjs';
// import MODEL_URL from '@/assets/model/model.json';

// const MODEL_URL = '@/assets/model/model.json';
// const model = await tf.loadLayersModel(MODEL_URL);

import Anggur from '@/assets/img/anggur.jpg';
import Apel from '@/assets/img/apel.jpg';
import Beras from '@/assets/img/beras.jpg';
import Buncis from '@/assets/img/buncis.jpeg';
import Delima from '@/assets/img/delima.jpg';
import Gude from '@/assets/img/gude.jpg';
import Jagung from '@/assets/img/jagung.jpg';
import Jeruk from "@/assets/img/jeruk.jpg";
import KacangHijau from "@/assets/img/kacang_hijau.jpg";
import KacangMatki from "@/assets/img/kacang_matki.jpeg";
import KacangMerah from "@/assets/img/kacang_merah.jpg";
import KacangUrad from "@/assets/img/kacang_urad.jpg";
import Kapas from "@/assets/img/kapas.jpg";
import Kelapa from "@/assets/img/kelapa.jpg";
import Kopi from "@/assets/img/kopi.jpg";
import Mangga from "@/assets/img/mangga.jpg";
import Melon from "@/assets/img/melon.jpg";
import MijuMiju from "@/assets/img/miju-miju.jpg";
import Pepaya from "@/assets/img/pepaya.jpg";
import Pisang from "@/assets/img/pisang.jpg";
import Rami from "@/assets/img/rami.jpeg";
import Semangka from "@/assets/img/semangka.jpg";

export default {
  name: 'HomeView',
  data() {
		return {
			temperature: '',
			humidity: '',
			ph: '',
			rainfall: '',
      recommend: '',
      submitted: false,
      crops: [
        {id: 1, name: "anggur", img: Anggur},
        {id: 2, name: "apel", img: Apel},
        {id: 3, name: "beras", img: Beras},
        {id: 4, name: "buncis", img: Buncis},
        {id: 5, name: "delima", img: Delima},
        {id: 6, name: "gude", img: Gude},
        {id: 7, name: "jagung", img: Jagung},
        {id: 8, name: "jeruk", img: Jeruk},
        {id: 9, name: "kacang hijau", img: KacangHijau},
        {id: 10, name: "kacang matki", img: KacangMatki},
        {id: 11, name: "kacang merah", img: KacangMerah},
        {id: 12, name: "kacang urad", img: KacangUrad},
        {id: 13, name: "kapas", img: Kapas},
        {id: 14, name: "kelapa", img: Kelapa},
        {id: 15, name: "kopi", img: Kopi},
        {id: 16, name: "mangga", img: Mangga},
        {id: 17, name: "melon", img: Melon},
        {id: 18, name: "miju-miju", img: MijuMiju},
        {id: 19, name: "pepaya", img: Pepaya},
        {id: 20, name: "pisang", img: Pisang},
        {id: 21, name: "rami", img: Rami},
        {id: 22, name: "semangka", img: Semangka}
      ]
		}
	},

	methods: {
		submitForm() {
      console.log("Form submitted");
      let x = Math.floor(Math.random() * 22);
      this.recommend = this.crops[x];
      this.submitted = !this.submitted;
		},
    isSubmitted() {
      // Reset value
      this.submitted = !this.submitted;
      this.temperature = '';
			this.humidity = '';
			this.ph = '';
			this.rainfall = '';
    }
	},

  components: {
    // tf,
    // MODEL_URL,
    Anggur,
    Apel,
    Beras,
    Buncis,
    Delima,
    Gude,
    Jagung,
    Jeruk,
    KacangHijau,
    KacangMatki,
    KacangMerah,
    KacangUrad,
    Kapas,
    Kelapa,
    Kopi,
    Mangga,
    Melon,
    MijuMiju,
    Pepaya,
    Pisang,
    Rami,
    Semangka
  }
}
</script>

<style>
h2 {
  color: blue;
  text-decoration: underline;
}
form, .result{
	max-width: 520px;
	margin: 20px auto;
	background: white;
	/* text-align: left; */
	padding: 10px;
	border-radius: 10px;
}
label {
	color: #555;
	display: inline-block;
	margin: 25px 0 15px;
	font-size: 0.5cm;
	letter-spacing: 1px;
	font-weight: bold;
}
input {
	display: block;
	padding: 10px 6px;
	width: 100%;
	box-sizing: border-box;
	border: 1px solid black;
	color: gray;
}
button {
	background: rgb(24, 178, 239);
	border: 0;
	padding: 10px 20px;
	margin-top: 20px;
	color: white;
	border-radius: 20px;
	text-transform: uppercase;
}
.submit {
	text-align: center;
}
img {
  border-radius: 50%;
  object-fit: cover;
  width: 460px;
  height: 460px;
}
</style>