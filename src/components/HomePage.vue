<template>
    <VigenereCipher v-if="showVigenereModal" @close="toggleVigenereModal" key="2"/>
    <GammaEncryption v-if="showGammaModal" @close="toggleGammaModal" key="1"/>
    
    <div class="w-full flex justify-around pt-10">
        <button @click="toggleVigenereModal" class="w-fit px-4 py-5 hover:bg-blue-400 duration-500 rounded-lg bg-blue-500">Show Vigenere Modal</button>

        <button @click="toggleGammaModal" class="w-fit px-4 hover:bg-blue-400 duration-500 rounded-lg  bg-blue-500">Show Gamma Modal</button>
    </div>
</template>

<script>
import VigenereCipher from './VigenereCipher.vue';
import GammaEncryption from './GammaEncryption.vue';

export default {
    data() {
        return {
            showVigenereModal: false,
            showGammaModal: false,
        }
    },
    components: {
        VigenereCipher,
        GammaEncryption
    },
    methods: {
        toggleVigenereModal() {
            this.showVigenereModal = !this.showVigenereModal;
        },
        toggleGammaModal() {
            this.showGammaModal = !this.showGammaModal;
        }
    }
}
</script>