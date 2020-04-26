<template>
  <div class="home">

    <v-container>

      <v-row justify="center" >
        <v-col xs="12" sm="6" md="4" lg="4" >
          <h1 class="black--text">Input Values</h1>
          <hr><br>
          <Form-cmp>
              <Select-cmp :labelName="'FONT'" :items="fonts" @selected="font = $event" :validations="[isEmpty]"></select-cmp>
              <Select-cmp :labelName="'COLOR'" :items="colors" @selected="color = $event" :validations="[isEmpty]"></select-cmp>
              <Select-cmp :labelName="'TRUEVIEW DPI'" :items="dpiList" @selected="dpi = $event" :validations="[isEmpty]"></select-cmp>
              <input-cmp  :labelName="'HEIGHT (IN)'" @input="height = $event" :validations="validations"></input-cmp>
              <text-area-cmp :labelName="'TEXT'" @input="text = $event" :validations="[isEmpty]"></text-area-cmp>
              <button-cmp :depressed="true" :name="'CREATE LETTERING'" :clickFn="handleSubmit"></button-cmp>
          </Form-cmp>
        </v-col>

        <v-col xs="12" sm="6" md="4" lg="4" >
          <h1 class="black--text" >Image Results</h1>
          <hr><br>
          <input-cmp  :labelName="'File'" @input="file = $event" ></input-cmp>
          <img :src="image" alt="">
          <p>{{convertToMM}}</p>
          <p>{{text}}</p>
          <p>{{font}}</p>
          <p>{{color}}</p>
          <p>{{dpi}}</p>
          <p>{{apiInfo}}</p>
        </v-col>
      </v-row>
  
    </v-container>
    

  </div>
</template>

<script>
// @ is an alias to /src
import InputCmp from '../components/Input.vue'
import SelectCmp from '../components/Select.vue'
import TextAreaCmp from '../components/Textarea.vue'
import FormCmp from '../components/Form.vue'
import ButtonCmp from '../components/Button.vue'
import image from '../../src/assets/img_place_holder.png'

export default {

  name: 'Home',
  data() {
    return {
      fonts: ['Athletica', 'engraver', 'fishtails', 'comics', 'Veranda'],
      colors: ['Red', 'Blue', "Green", "Black", "Gold"],
      dpiList: [72, 96, 128, 150, 192],
      validations: [this.isEmpty, this.isNumber, this.inRange],
      font: "",
      color: "",
      dpi: "",
      height: 0.0,
      text: "",
      apiInfo: "",
      file: "",
      image: image
    }
  },
  components: {
    InputCmp,
    FormCmp,
    SelectCmp,
    ButtonCmp,
    TextAreaCmp
  },
  computed: {
    convertToMM() {
      return parseFloat(this.height) * 25.4
    }
  },
  methods: {
    isEmpty(val) {
        if (val === "") {
          return 'Field cannot be empty'
        } else {
          return true
        }
    },
    isNumber(val) {
        if(isNaN(val)) {
          return "Input must be a number"
        } else {
          return true
        }
    },
    inRange(val) {
        let num = parseFloat(val)

        if (num >= 0.19685 && num <= 1.9685) {
          return true 
        } else {
          return "Please enter the number between 0.19685 to 1.9685"
        }
    },
    handleSubmit() {
      this.axios
        .get('https://api.coindesk.com/v1/bpi/currentprice.json')
        .then(response => (this.apiInfo = response))
    } 
  }
}
</script>

<style  scoped>

 

   
</style>
