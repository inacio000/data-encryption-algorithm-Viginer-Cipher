<template>
    <dii @click.self="closeModal" class="w-full h-full fixed bg-modalbg">
        <div class="flex flex-col items-center text-center max-w-md my-6 mx-auto bg-white p-6 rounded-lg relative">
            <h1 class="text-labelColor inline-block my-2 text-md uppercase font-bold">Gamma Cipher</h1>
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
    </dii>
</template>

<script>

export default {
    data() {
        return {
            message: '',
            key: '',
            result: '',
            showModal: true,
        };
    },
    methods: {
        closeModal() {
            this.$emit('close')
        },
        gammaEncrypt(mensagem, chave) {
            let mensagemCifrada = "";
            for (let i = 0; i < mensagem.length; i++) {
                const charDaMensagem = mensagem.charCodeAt(i);
                const charDaChave = chave.charCodeAt(i % chave.length);
                const charCriptografado = charDaMensagem + charDaChave;
                mensagemCifrada += String.fromCharCode(charCriptografado);
            }
            return mensagemCifrada;
        },
        gammaDecrypt(mensagemCifrada, chave) {
            let mensagemOriginal = "";
            for (let i = 0; i < mensagemCifrada.length; i++) {
                const charDaMensagemCifrada = mensagemCifrada.charCodeAt(i);
                const charDaChave = chave.charCodeAt(i % chave.length);
                const charDescriptografado = charDaMensagemCifrada - charDaChave;
                mensagemOriginal += String.fromCharCode(charDescriptografado);
            }
            return mensagemOriginal;
        },
        encryptMessage() {
            const encryptedMessage = this.gammaEncrypt(this.message, this.key);
            this.result = `Mensagem Criptografada: ${encryptedMessage}`
        },
        decryptMessage() {
            const decryptedMessage = this.gammaDecrypt(this.message, this.key);
            this.result = `Mensagem Descriptografada: ${decryptedMessage}`;
        }
    }
}
</script>