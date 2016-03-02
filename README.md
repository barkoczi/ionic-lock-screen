# ionic-lock-screen

<img src="https://raw.githubusercontent.com/AlexDisler/ionic-lock-screen/master/ionic-lock-screen.gif"/>

## Features

- Supports [Touch ID](https://github.com/AlexDisler/ionic-lock-screen#touch-id-ios-only) on iOS using [cordova-plugin-touchid](https://github.com/leecrossley/cordova-plugin-touchid)
- [Customizable](https://github.com/AlexDisler/ionic-lock-screen#theming--language)

## Install

### Bower

    $ bower install qm-ionic-lock-screen --save

## Use

Include as a dependency in your angular module

```js
angular.module('myApp', ['ionic-lock-screen'])
```

Add the directive as the first element in your app container element:

```html
<body ng-app="myApp">
  <lock-screen></lock-screen>
  ...
</body>
```
Note: add <lock-screen> tag after body tag, not in any <ng-view>. 

Load whenever the app is opened:

```js
.run(['$lockScreen', $ionicPlatform, function($lockScreen, $ionicPlatform) {
    $ionicPlatform.ready(function() {
      $lockScreen.show({
        code: '1234',
        onCorrect: function () {
          console.log('correct!');
        },
        onWrong: function (attemptNumber) {
          console.log(attemptNumber + ' wrong passcode attempt(s)');
        },
      });
    });
}]);
```
or add use in you controller file: 

```js
function Mycontroller ($lockScreen){
  var vm = this;

  vm.askPassCode = function(){
    $lockScreen.show({
          code: '1234',
          onCorrect: function () {
              //yeah, you are in, redirect user to the requested page
        },
        onWrong: function (attemptNumber) {
          // after 3 attempt you notify the user and hide the lock screen
          if(attemptNumber == 3){
             //hide lock screen
             $lockScreen.hide();
             alert("Sorry, you are not authorized to reach the requested page!");
           }
        }
        });

  };
}
Mycontroller.$inject = ['$lockScreen'];

angular.module('main').controller('Mycontroller', Mycontroller);

```


You can also trigger the lock screen on the [resume](https://cordova.apache.org/docs/en/latest/cordova/events/events.resume.html) and [pause](https://cordova.apache.org/docs/en/latest/cordova/events/events.pause.html) events.

## Touch ID (iOS only)

<img src="https://raw.githubusercontent.com/AlexDisler/ionic-lock-screen/master/lock-screen-passcode.png"/>

Install [cordova-plugin-touchid](https://github.com/leecrossley/cordova-plugin-touchid)

    $ cordova plugin add cordova-plugin-touchid --save

Set ```touchId:true```

```js
$lockScreen.show({
  code: '1234',
  touchId: true,
});
```

### Theming / Language

See available options [here](https://github.com/AlexDisler/ionic-lock-screen/blob/master/src/lock-screen/lock-screen.js#L9-L15).

# License

MIT
