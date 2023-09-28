<template>
    <div @click.self="closeModal" class="w-full h-full fixed bg-modalbg">
        <div class="flex flex-col items-center text-center max-w-md my-6 mx-auto bg-white p-6 rounded-lg relative">
            <slot name="form"></slot>

            <span @click="closeModal"
                class="cursor-pointer absolute top-0 right-0 m-4 px-1 border rounded hover:bg-gray-100 duration-300">X</span>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        closeModal() {
            this.$emit('close')
        }
    }
}
</script>