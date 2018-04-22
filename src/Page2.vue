<template>
  <v-ons-page>
    <custom-toolbar>Page 1</custom-toolbar>
    <p style="text-align: center">
      This is the first page
      <v-ons-button @click="push">Push Page 2</v-ons-button>
    </p>
    <h1 class="text-center">Demo of vue-touch-keyboard</h1>
    <div class="container" id="app">
      {{text1}} &nbsp;&nbsp;{{text2}}

      <fieldset>
        <legend>Normal layout</legend>
        <input type="text" placeholder="Text input" @focus="show" v-model="text1"   data-layout="normal" />
      </fieldset>

      <fieldset>
        <legend>Compact layout</legend>
        <input type="text" placeholder="Text input" @focus="show" v-model="text2" data-layout="compact" />
      </fieldset>

      <fieldset>
        <legend>Numeric layout</legend>
        <input type="text" placeholder="Text input" @focus="show" data-layout="numeric" />
      </fieldset>

      <vue-touch-keyboard id="keyboard" v-if="visible" :layout="layout" :cancel="hide" :accept="accept" :input="input" :next="next" />

    </div>
  </v-ons-page>
</template>

<script>
  import Vue from 'vue';
  import customToolbar from './CustomToolbar';
  import page1 from './Page3';
  import VueTouchKeyboard from "vue-touch-keyboard";
  import style from "vue-touch-keyboard/dist/vue-touch-keyboard.css"; // load default style

  Vue.use(VueTouchKeyboard);

  export default {
    data(){
      return {
        text1:'',
        text2:'',
        visible: false,
        layout: "normal",
        input: null,
        options: {
          useKbEvents: false
         }
        }
      },
    methods: {

      push() {
        this.pageStack.push(page1);
      },
      pop() {
        this.pageStack.pop();
      },
      accept(text) {
        console.log("Input text: " + text);
        this.hide();
      },

      show(e) {
        document.addEventListener('deviceready', function() {
          Keyboard.hide();
          Keyboard.shrinkView(true)
          Keyboard.hideFormAccessoryBar(value, successCallback);
          window.addEventListener('keyboardDidShow', function () {
            document.activeElement.scrollIntoView()
          })
        })
        this.input = e.target;
        this.layout = e.target.dataset.layout;

        if (!this.visible)
          this.visible = true
      },

      hide() {
        this.visible = false;
      },

      next() {
        let inputs = document.querySelectorAll("input");
        let found = false;
        [].forEach.call(inputs, (item, i) => {
          if (!found && item == this.input && i < inputs.length - 1) {
            found = true;
            this.$nextTick(() => {
              inputs[i+1].focus();
            });
          }
        });
        if (!found) {
          this.input.blur();
          this.hide();
        }
      }
    },
    props: ['pageStack'],
    components: { customToolbar }
  }
</script>
