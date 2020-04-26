<template>
    <v-text-field outlined :rules="validations" v-model="value" @change="inputChanged" :label="labelName"></v-text-field>
</template>

<script>
export default {
    props:['type', 'labelName', 'validations'],
    data() {
        return {
            value: "",
        }
    },
    methods: {
        inputChanged() {
            return this.$emit('input', this.value)  
        }
    },
    
    
}
</script>

