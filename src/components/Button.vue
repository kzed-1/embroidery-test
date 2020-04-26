<template>
    <v-btn :depressed="depressed" dark color="pink" @click="clickFn"> 
        {{ name }}
    </v-btn>
</template>

<script>
export default {
    props:['name', 'depressed', 'clickFn']
    
}
</script>

