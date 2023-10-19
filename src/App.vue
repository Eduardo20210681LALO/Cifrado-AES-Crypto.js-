<template>
  <div id="app">
    <div>
      <label for="texto">Texto:</label>
      <input v-model="cifrado" id="texto" type="text" @input="escribir" />
    </div>
    <div>
      <button @click="cifrar">Cifrar</button>
      <button @click="descifrar">Descifrar</button>
    </div>
    <div v-if="resultado">
      <label for="resultado">Resultado:</label>
      <input v-model="resultado" id="resultado" type="text" readonly />
    </div>
  </div>
</template>

<script>
import CryptoJS from 'crypto-js';

export default {
  data() {
    return {
      cifrado: '',
      resultado: '',
      contra: 'Eduardo20210681EHH'
    };
  },
  methods: {
    escribir(event) {
      this.cifrado = event.target.value;
    },
    cifrar() {
      const ciphertext = CryptoJS.AES.encrypt(this.cifrado, this.contra).toString();
      this.resultado = ciphertext;
    },
    descifrar() {
      const bytes = CryptoJS.AES.decrypt(this.resultado, this.contra);
      const originalData = bytes.toString(CryptoJS.enc.Utf8);
      this.resultado = originalData;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input {
  margin-bottom: 10px;
  padding: 5px;
  width: 200px;
}
</style>
