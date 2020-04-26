<template>
    <v-textarea outlined :label="labelName" :rules="validations" v-model="value" @change="inputChanged"></v-textarea>
</template>

<script>
export default {
    props:['labelName', 'validations'],
    data() {
        return {
            value: ""
        }
    },
    methods: {
        inputChanged() {
            return this.$emit('input', this.value)  
        }
    }
    
}
</script>

