<template>
  <v-ons-page>
    <custom-toolbar :back-label="'Page 2'">Page 2</custom-toolbar>
    <!--<keyboard-->
            <!--v-model="input"-->
            <!--@custom="custom"-->
            <!--@input="changed"-->
            <!--:layouts="[-->
		<!--'1234567890{delete:backspace}|qwertyuiop|asdfghjkl|{shift:goto:1}zxcvbnm|{space:space}{custom:custom}',-->
		<!--'!@#$%^&*(){delete:backspace}|QWERTYUIOP|ASDFGHJKL|{shift:goto:0}ZXCVBNM|{space:space}{custom:custom}'-->
	<!--]"-->
            <!--:maxlength="16"-->
    <!--&gt;</keyboard>-->
    <div id="header">
      <div id="title">Chatting with John</div>
      <div id="toggleChat" @click="toggleChat()">Toggle</div>
      <div id="focusMessenger" @click="showMessengerKeyboard()">Focus</div>
      <div id="updateMessenger" @click="updateMessenger()">Update</div>
    </div>

    <div id="messages">
      <div class="message left"><span>Long time no chat!</span>
        <div>10/19/16, 2:18 AM</div>
      </div>
      <div class="message right"><span>Yeah likewise ;)</span>
        <div>10/20/16, 4:15 PM</div>
      </div>
      <div class="message left"><span>Hey man, how are you?</span>
        <div>10/20/16, 4:18 PM</div>
      </div>
      <div class="message right"><span>Good, thanks, how are you?</span>
        <div>10/20/16, 4:20 PM</div>
      </div>
      <div class="message left"><span>Meh.. could be better. I'm out of beer 🍺. Do you have any left?</span></div>
      <div class="message left"><span>.. please!</span>
        <div>10/20/16, 4:21 PM</div>
      </div>
      <div class="message right"><span>Lemme check..</span></div>
      <div class="message right"><span>Dude! I have 2 sixpacks stacked in the fridge - come over! 🍻</span>
        <div>10/20/16, 4:23 PM</div>
      </div>
      <div class="message left"><span>Right on! Let's party 🎉 🎉</span>
        <div>10/20/16, 4:23 PM</div>
      </div>
    </div>
  </v-ons-page>
</template>

<script>

  function hideMessenger() {
    NativeKeyboard.hideMessenger({
      animated: true
    });
  }
  function updateMessenger() {
    var options = {
      text: "This is the updated text! ",
      showKeyboard: true,
      caretIndex: 10 // caret is set at end of text if not specified
    };
    NativeKeyboard.updateMessenger(
      options,
      // optional success and error handlers
      function(){},
      function(){});
  }
  function showMessengerKeyboard() {
    NativeKeyboard.showMessengerKeyboard(function(){}, function(){});
  }
  function showMessenger() {
    var options = {
      onSubmit: function (text) {
        console.log("onSubmit: " + text);
        appendMessage(text);
      },
      onKeyboardWillShow: function (height) {
        console.log("keyboard will show, height is: " + height);
        //appendMessage("keyboard will show, height is: " + height);
      },
      onKeyboardDidShow: function (height) {
        console.log("keyboard shows, height is: " + height);
        //appendMessage("keyboard shows, height is: " + height);
      },
      onKeyboardWillHide: function () {
        console.log("keyboard will hide");
      },
      onKeyboardDidHide: function () {
        console.log("keyboard did hide");
      },
      onTextChanged: function(newText) {
        console.log("text changed to: " + newText);
        //appendMessage(newText);
      },
      showKeyboard: true,
      type: "twitter", // iOS only, default (default) | decimalpad | phonepad | numberpad | namephonepad | number | email | twitter | url | alphabet | search | ascii
      appearance: "light", // iOS only,  light (default) | dark
      secure: false, // iOS only,  default false, disables things like Emoji and Predicive text entry
      autocorrectionEnabled: false, // on iOS this hides the 'predictive text' bar
      scrollToBottomAfterMessengerShows: true,
      autoscrollElement: document.getElementById("messages"), // default unset
      keepOpenAfterSubmit: true, // default false
      animated: true,
      text: "This has been prefilled",
      placeholder: 'Type your message..',
      placeholderColor: "#DDDDDD",
      suppressSuggestions: true, // default true
      textViewBackgroundColor: "#F6F6F6",
      backgroundColor: "#F6F6F6", // default #F7F7F7
      textViewBorderColor: "#777777", // iOS only
      maxChars: 140, // setting this > 0 will make the counter show up on iOS (and ignore input on Android, for now)
      counterStyle: 'countdownreversed', // iOS only currently, note that 'none' still shows a counter in case maxChars is set
      textColor: '#555555',
      // this button is best suited for picking media (camera / cameraroll / last image) from an actionsheet
      leftButton: {
        type: 'ionicon', // or 'text' (Android only currently) or 'fontawesome'
        value: '\uf48a', // http://ionicons.com/ - right-click and inspect the :before value (don't forget the \uf !)
        //color: '#ff0000', // default blue on iOS, grey on Android
        textStyle: 'normal', // if type is 'text', you can set this to 'normal' (default), 'bold', 'italic'
        disabledWhenTextEntered: false, // default false
        onPress: function () {
          if (window.plugins && window.plugins.actionsheet) {
            window.plugins.actionsheet.show({
              androidTheme: window.plugins.actionsheet.ANDROID_THEMES.THEME_DEVICE_DEFAULT_LIGHT,
              buttonLabels: ['Take Photo or Video', 'Use Last Photo Taken', 'Choose From Library'],
              addCancelButtonWithLabel: 'Cancel'
            }, function(index) {
              if (index != 4) { // which is 'cancel'
                console.log("Picked index " + index + ".. you'll need to implement the rest yourself ;)");
              }
            });
          } else {
            alert("Left button pressed - if you install cordova-plugin-actionsheet you'll see a nice ActionSheet in this demo.");
          }
        }
      },
      rightButton: {
        type: 'text', // or 'fontawesome' or 'ionicon', default 'text'
        value: 'Send', // 'fa-battery-quarter', // '\uf2c3', // 'Send', // default 'Send'
        textStyle: 'bold', // 'normal' (default), 'bold', 'italic'
        //color: '#FF0000', // default iOS blue
        onPress: function () {
          console.log("Right button was pressed - text was passed to 'onSubmit' if provided.");
        }
      }
    };
    var onSuccess = function () {
      console.log("Show Messenger succeeded!");
    };
    var onError = function (message) {
      console.log("Got error message: " + message);
    };
    NativeKeyboard.showMessenger(options, onSuccess, onError);
  }
  function toggleChat() {
    if (chatShowing) {
      hideMessenger();
    } else {
      showMessenger();
    }
    chatShowing = !chatShowing;
  }
  var chatShowing = true;
  if (chatShowing) {
    document.addEventListener('deviceready', showMessenger, false);
  }


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
      },
      hideMessenger() {
        NativeKeyboard.hideMessenger({
          animated: true
        });
      },
      aupdateMessenger() {
        var options = {
          text: "This is the updated text! ",
          showKeyboard: true,
          caretIndex: 10 // caret is set at end of text if not specified
        };
        NativeKeyboard.updateMessenger(
          options,
          // optional success and error handlers
          function(){},
          function(){});
      },
      ashowMessengerKeyboard() {
        NativeKeyboard.showMessengerKeyboard(function(){}, function(){});
      },
      ashowMessenger() {
        var options = {
          onSubmit: function (text) {
            console.log("onSubmit: " + text);
            appendMessage(text);
          },
          onKeyboardWillShow: function (height) {
            console.log("keyboard will show, height is: " + height);
            //appendMessage("keyboard will show, height is: " + height);
          },
          onKeyboardDidShow: function (height) {
            console.log("keyboard shows, height is: " + height);
            //appendMessage("keyboard shows, height is: " + height);
          },
          onKeyboardWillHide: function () {
            console.log("keyboard will hide");
          },
          onKeyboardDidHide: function () {
            console.log("keyboard did hide");
          },
          onTextChanged: function (newText) {
            console.log("text changed to: " + newText);
            //appendMessage(newText);
          },
          showKeyboard: true,
          type: "twitter", // iOS only, default (default) | decimalpad | phonepad | numberpad | namephonepad | number | email | twitter | url | alphabet | search | ascii
          appearance: "light", // iOS only,  light (default) | dark
          secure: false, // iOS only,  default false, disables things like Emoji and Predicive text entry
          autocorrectionEnabled: false, // on iOS this hides the 'predictive text' bar
          scrollToBottomAfterMessengerShows: true,
          autoscrollElement: document.getElementById("messages"), // default unset
          keepOpenAfterSubmit: true, // default false
          animated: true,
          text: "This has been prefilled",
          placeholder: 'Type your message..',
          placeholderColor: "#DDDDDD",
          suppressSuggestions: true, // default true
          textViewBackgroundColor: "#F6F6F6",
          backgroundColor: "#F6F6F6", // default #F7F7F7
          textViewBorderColor: "#777777", // iOS only
          maxChars: 140, // setting this > 0 will make the counter show up on iOS (and ignore input on Android, for now)
          counterStyle: 'countdownreversed', // iOS only currently, note that 'none' still shows a counter in case maxChars is set
          textColor: '#555555',
          // this button is best suited for picking media (camera / cameraroll / last image) from an actionsheet
          leftButton: {
            type: 'ionicon', // or 'text' (Android only currently) or 'fontawesome'
            value: '\uf48a', // http://ionicons.com/ - right-click and inspect the :before value (don't forget the \uf !)
            //color: '#ff0000', // default blue on iOS, grey on Android
            textStyle: 'normal', // if type is 'text', you can set this to 'normal' (default), 'bold', 'italic'
            disabledWhenTextEntered: false, // default false
            onPress: function () {
              if (window.plugins && window.plugins.actionsheet) {
                window.plugins.actionsheet.show({
                  androidTheme: window.plugins.actionsheet.ANDROID_THEMES.THEME_DEVICE_DEFAULT_LIGHT,
                  buttonLabels: ['Take Photo or Video', 'Use Last Photo Taken', 'Choose From Library'],
                  addCancelButtonWithLabel: 'Cancel'
                }, function (index) {
                  if (index != 4) { // which is 'cancel'
                    console.log("Picked index " + index + ".. you'll need to implement the rest yourself ;)");
                  }
                });
              } else {
                alert("Left button pressed - if you install cordova-plugin-actionsheet you'll see a nice ActionSheet in this demo.");
              }
            }
          },
          rightButton: {
            type: 'text', // or 'fontawesome' or 'ionicon', default 'text'
            value: 'Send', // 'fa-battery-quarter', // '\uf2c3', // 'Send', // default 'Send'
            textStyle: 'bold', // 'normal' (default), 'bold', 'italic'
            //color: '#FF0000', // default iOS blue
            onPress: function () {
              console.log("Right button was pressed - text was passed to 'onSubmit' if provided.");
            }
          }
        }
        var onSuccess = function () {
          console.log("Show Messenger succeeded!");
        };
        var onError = function (message) {
          console.log("Got error message: " + message);
        };
        NativeKeyboard.showMessenger(options, onSuccess, onError);
      },
      atoggleChat() {
        if (chatShowing) {
          hideMessenger();
        } else {
          showMessenger();
        }
        chatShowing = !chatShowing;
      },
      // var chatShowing = true;
      // if (chatShowing) {
      //   document.addEventListener('deviceready', showMessenger, false);
      // }

     },
     props: ['pageStack'],
     components: { customToolbar,keyboard }
  }
</script>

<style scoped>
  * {
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0); /* make transparent link selection, adjust last value opacity 0 to 1.0 */
  }
  body {
    -webkit-touch-callout: none; /* prevent callout to copy image, etc when tap to hold */
    -webkit-text-size-adjust: none; /* prevent webkit from resizing text to fit */
    -webkit-user-select: none; /* prevent copy paste, to allow, change 'none' to 'text' */
    background-color: #E4E4E4;
    font-family: 'HelveticaNeue-Light', 'HelveticaNeue', Helvetica, Arial, sans-serif;
    font-size: 16px;
    height: 100%;
    padding: 0;
    margin: 0;
    width: 100%;
  }
  #header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #DDDDDD;
    border-bottom: 1px solid #BBBBBB;
    height: 60px;
    z-index: 2;
  }
  #header #title {
    position: absolute;
    top: 20px;
    left: 20px;
  }
  #header #toggleChat {
    position: absolute;
    top: 26px;
    background-color: #eee;
    right: 0;
    font-size: 12px;
    text-decoration: underline;
    padding: 2px;
    border-radius: 2px;
  }
  #header #focusMessenger {
    position: absolute;
    top: 26px;
    background-color: #eee;
    right: 44px;
    font-size: 12px;
    text-decoration: underline;
    padding: 2px;
    border-radius: 2px;
  }
  #header #updateMessenger {
    position: absolute;
    top: 26px;
    background-color: #eee;
    right: 86px;
    font-size: 12px;
    text-decoration: underline;
    padding: 2px;
    border-radius: 2px;
  }
  #messages {
    width: 96%;
    left: 2%;
    position: absolute;
    top: 60px;
    bottom: 0;
    overflow-y: scroll;
  }
  .message {
    width: 100%;
    padding: 4px 0;
  }
  .right {
    text-align: right;
  }
  .message span {
    width: 65%;
    padding: 14px 10px;
    border-radius: 5px;
    display: inline-block;
    /*margin: 0 20px;*/
    text-align: left;
  }
  .message div {
    padding: 6px 10px;
    display: inline-block;
    margin: 0 20px 8px 20px;
    color: #BBBBBB;
    font-size: 12px;
  }
  .message.left span {
    background-color: #CCCCCC;
  }
  .message.right span {
    color: #FFFFFF;
    background-color: #007AFF;
  }

</style>
