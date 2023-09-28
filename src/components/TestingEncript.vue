<template>
  <div>
    <h1>Cifra de Vigenère</h1>
    
    <input v-model="message" placeholder="Mensagem" />

    <input v-model="key" placeholder="Chave" />

    <button @click="encrypt">Criptografar</button>
    <button @click="decrypt">Descriptografar</button>

    <div>
      <p>Mensagem Criptografada: {{ encryptedMessage }}</p>
      <p>Mensagem Descriptografada: {{ decryptedMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "",
      key: "",
      encryptedMessage: "",
      decryptedMessage: ""
    };
  },
  methods: {
    encrypt() {
      this.encryptedMessage = this.vigenere(this.message, this.key, true);
    },
    decrypt() {
      this.decryptedMessage = this.vigenere(this.encryptedMessage, this.key, false);
      console.log(this.decryptedMessage)
    },
    vigenere(text, key, encrypt) {
      let result = "";
      const textLength = text.length;
      const keyLength = key.length;

      for (let i = 0; i < textLength; i++) {
        const textChar = text.charCodeAt(i);
        const keyChar = key.charCodeAt(i % keyLength);
        const shift = encrypt ? keyChar - 65 : 26 - (keyChar - 65);
        const encryptedChar = String.fromCharCode(((textChar - 65 + shift) % 26) + 65);
        result += encryptedChar;
      }

      return result;
    }
  }
};
</script>
