<template>
    <v-ons-page>
        <custom-toolbar :back-label="'Page 2'">Page 2</custom-toolbar>
        <div id="deviceready" class="blink">
            <p class="event listening">Connecting to Device</p>

            <br/><input type="text" value="regular input" maxlength="15" style="font-size:13px; font-family:Helvetica; font-style:italic" /><br/><br/>

            <br/><input data-nativekeyboard="true" type="text" value="max 15 chars" maxlength="15" style="font-size:13px; font-family:Helvetica; font-style:italic" /><br/><br/>

            <br/><input data-nativekeyboard='{"type":"decimal", "maxlength":4}' type="text" value="100" style="font-family: Verdana; font-size:15px; font-weight: bold" /><br/><br/>

            <br/><input data-nativekeyboard='{"type":"numbersandpunctuation", "accessorybar":{}}' type="number" value="200" style="font-family: Verdana; font-size:15px; font-weight: bold" /><br/><br/>

            <br/><input data-nativekeyboard='{"type":"decimal"}' type="text" value="19.95" style="font-family: Arial; font-size:15px; font-weight: bold" /><br/><br/>

            <br/><input data-nativekeyboard='configureNativeKeyboard("#FF0000")' type="tel" value="+31650123456" style="font-family: Arial; font-size:15px; font-weight: bold" /><br/><br/>

            <br/><input data-nativekeyboard='configureNativeKeyboard' type="email" value="sergey@google.com" style="font-family: Arial; font-size:12px; font-weight: normal" /><br/><br/>

            <br/><input data-nativekeyboard='{"type":"twitter"}' type="text" value="@eddyverbruggen" style="font-family: Arial; font-size:12px; font-weight: normal; color: #FF0000" /><br/><br/>

            <br/><textarea data-nativekeyboard='{}' style="font-size:15px; font-family:Helvetica; font-weight: bold; border-radius:0">Helvetica</textarea><br/><br/>

            <br/><textarea data-nativekeyboard='{}' style="font-size:15px; font-family:Arial; border-radius:5px">Arial, with border radius</textarea><br/><br/>

            <!--br/><div data-nativekeyboard='{"type":"default"}' id="content" onclick="window.plugins.toast.editText(this)" style="width:200px;height:50px;background-color:#ddd;text-transform:none">12345</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"decimal"}' id="content2" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; border:4px solid red; font-family: Arial; width:160px; height:50px; color:#fff; background-color:#000; text-transform:none">9,95</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"phone"}' id="content3" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; padding:4px; font-family: Arial; width:160px; height:50px; color:#fff; background-color:#000; text-transform:none">0650298958</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"number"}' id="content4" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; margin: 4px; font-family: Arial; width:160px; height:50px; color:#fff; background-color:#000; text-transform:none">112233</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"namephone"}' id="content5" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Arial; width:160px; height:50px; color:#222; background-color:#fff; text-transform:none">namephone</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"numberspunc"}' id="content6" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Helvetica; width:160px; height:50px; color:#ddd; background-color:#555; text-transform:none">numberspunc</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"twitter"}' id="content6" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Helvetica; width:160px; height:50px; color:#ddd; background-color:#555; text-transform:none">twitter</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"email"}' id="content6" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Helvetica; width:160px; height:50px; color:#ddd; background-color:#555; text-transform:none">email</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"url"}' id="content6" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Helvetica; width:160px; height:50px; color:#ddd; background-color:#555; text-transform:none">url</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"alphabet"}' id="content6" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Helvetica; width:160px; height:50px; color:#ddd; background-color:#555; text-transform:none">alphabet</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"search"}' id="content6" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Helvetica; width:160px; height:50px; color:#ddd; background-color:#555; text-transform:none">search</div><br/><br/>
             <br/><div data-nativekeyboard='{"type":"ascii"}' id="content6" onclick="window.plugins.toast.editText(this)" style="font-size: 16px; font-family: Helvetica; width:160px; height:50px; color:#ddd; background-color:#555; text-transform:none">ascii</div><br/><br/-->

            <p class="event received">Device is Ready</p>
            <br/>
            <button onclick="showMessenger()">show messenger</button>&nbsp;
            <button onclick="NativeKeyboard.hideMessenger({animated:true})">hide</button>
            <br/>
            <div id="messages">First<br/><br/>Second<br/><br/>Third</div>
            <br/>
            <br/>
            <br/>
            <br/>
        </div>
    </v-ons-page>
</template>

<script>


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
