<template>
    <v-select outlined :label="labelName" :items="items" v-model="value" @change="inputSelected" :rules="validations"></v-select>
</template>

<script>
export default {
   props: ['labelName', 'items', 'validations'],
   data() {
       return {
           value: ""
       }
   }, 
   methods: {
       inputSelected() {
           return this.$emit('selected', this.value)
       }
   }
    
}
</script>

