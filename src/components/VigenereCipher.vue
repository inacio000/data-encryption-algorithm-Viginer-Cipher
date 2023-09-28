<template>
    <div @click.self="closeModal" class="w-full h-full fixed bg-modalbg">
        <div 
            class="flex flex-col items-center text-center max-w-md my-6 mx-auto bg-white p-6 rounded-lg relative">
            <h1 class="text-labelColor inline-block my-2 text-md uppercase font-bold">Viginer Cipher</h1>
            <label class="w-full text-start text-labelColor mt-2 text-sm font-bold">Mensagem:</label>
            <input type="text" class="w-full block px-2 py-3 box-border border-b-2 border-inputBorder text-inputColor mb-6"
                v-model="message">

            <label class="w-full text-start text-labelColor mt-2 text-sm font-bold">Chave:</label>
            <input type="text" class="w-full block px-2 py-3 box-border border-b-2 border-inputBorder text-inputColor mb-6"
                v-model="key" />

            <div class="flex gap-4 flex-wrap justify-center items-center">
                <button @click="encryptMessage"
                    class="bg-blue-600 py-2 px-4 mt-2 text-white rounded-3xl">Criptografar</button>
                <button @click="decryptMessage"
                    class="bg-blue-600 py-2 px-4 mt-2 text-white rounded-3xl">Descriptografar</button>
            </div>
            <h2 class="text-labelColor inline-block my-5 border-b-4 text-sm uppercase font-bold">Resultado</h2>
            <div><span class="font-bold">{{ result }}</span></div>
            <span @click="closeModal"
            class="cursor-pointer absolute top-0 right-0 m-4 px-1 border rounded hover:bg-gray-100 duration-300">X</span>
        </div>
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
        closeModal() {
            this.$emit('close')
        },
        vigenereEncrypt(message, key) {
            let encryptedMessage = '';
            const keyLength = key.length;

            for (let i = 0; i < message.length; i++) {
                const char = message.charAt(i);
                let charCodeA;

                if (char >= 'A' && char <= 'Z') {
                    charCodeA = 'A'.charCodeAt(0);
                } else if (char >= 'a' && char <= 'z') {
                    charCodeA = 'a'.charCodeAt(0);

                } else {
                    encryptedMessage += char;
                    continue;
                }
                const messageChar = char.charCodeAt(0);
                const keyChar = key.charCodeAt(i % keyLength);
                const encryptedChar = String.fromCharCode(((messageChar - charCodeA + keyChar - charCodeA) % 26) + charCodeA);
                encryptedMessage += encryptedChar;
            }

            return encryptedMessage;
        },
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
                    decryptedMessage += char;
                }
            }

            return decryptedMessage;
        },

        encryptMessage() {
            const encryptedMessage = this.vigenereEncrypt(this.message, this.key);
            this.result = `Mensagem Criptografada: ${encryptedMessage}`
        },
        decryptMessage() {
            const decryptedMessage = this.vigenereDecrypt(this.message, this.key);
            this.result = `Mensagem Descriptografada: ${decryptedMessage}`;
        },
    }
}
</script>