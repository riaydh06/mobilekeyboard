<template>
  <v-ons-page>
    <custom-toolbar :back-label="'Page 2'">Page 2</custom-toolbar>
    <keyboard
            v-model="input"
            @custom="custom"
            @input="changed"
            :layouts="[
		'1234567890{delete:backspace}|qwertyuiop|asdfghjkl|{shift:goto:1}zxcvbnm|{space:space}{custom:custom}',
		'!@#$%^&*(){delete:backspace}|QWERTYUIOP|ASDFGHJKL|{shift:goto:0}ZXCVBNM|{space:space}{custom:custom}'
	]"
            :maxlength="16"
    ></keyboard>
  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import keyboard from 'vue-keyboard';
  export default {
    data() {
      return {
        input: ''
      }
    },
    methods: {
      changed(value) {
        console.log('Value ' + value);
      },

      custom(keyboard) {
        console.log(keyboard.value);
      },
      pop(){
        this.pageStack.pop();
      }
     },
     props: ['pageStack'],
     components: { customToolbar,keyboard }
  }
</script>
