<template>
    <div>
        <h1>Vigenère Cipher</h1>
        <label for="message">Mensagem:</label>
        <textarea id="message" rows="3" cols="50" v-model="message"></textarea>

        <label for="key">Chave:</label>
        <input type="text" id="key" v-model="key" />

        <button @click="encryptMessage">Criptografar</button>
        <button @click="decryptMessage">Descriptografar</button>
        <h2>Resultado:</h2>
        <div id="result">{{ result }}</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: '',
            key: '',
            result: '',
        };
    },
    methods: {
        vigenereEncrypt(message, key) {
            let encryptedMessage = '';
            const keyLength = key.length;

            for (let i = 0; i < message.length; i++) {
                const char = message.charAt(i);
                const charCodeA = 'A'.charCodeAt(0);

                if (char >= 'A' && char <= 'Z') {
                    const messageChar = char.charCodeAt(0);
                    const keyChar = key.charCodeAt(i % keyLength);
                    const encryptedChar = String.fromCharCode(((messageChar - charCodeA + keyChar - charCodeA) % 26) + charCodeA);
                    encryptedMessage += encryptedChar;
                } else {
                    // Se o caractere não for uma letra maiúscula, mantenha-o inalterado
                    encryptedMessage += char;
                }
            }

            return encryptedMessage;
        },

        // Função para descriptografar uma mensagem usando o Vigenère Cipher
        vigenereDecrypt(encryptedMessage, key) {
            let decryptedMessage = '';
            const keyLength = key.length;

            for (let i = 0; i < encryptedMessage.length; i++) {
                const char = encryptedMessage.charAt(i);
                const charCodeA = 'A'.charCodeAt(0);

                if (char >= 'A' && char <= 'Z') {
                    const encryptedChar = char.charCodeAt(0);
                    const keyChar = key.charCodeAt(i % keyLength);
                    const decryptedChar = String.fromCharCode(((encryptedChar - charCodeA - keyChar + 26) % 26) + charCodeA);
                    decryptedMessage += decryptedChar;
                } else {
                    // Se o caractere não for uma letra maiúscula, mantenha-o inalterado
                    decryptedMessage += char;
                }
            }

            return decryptedMessage;
        },

        encryptMessage() {
            const encryptedMessage = this.vigenereEncrypt(this.message, this.key);
            this.result = `Mensagem Criptografada: ${encryptedMessage}`;
            console.log(encryptedMessage)
        },
        decryptMessage() {
            const decryptedMessage = this.vigenereDecrypt(this.message, this.key);
            this.result = `Mensagem Descriptografada: ${decryptedMessage}`;
        },
    }
}
</script>