# Javascript Design Patterns


Design patterns is a recipe for how to solve a problem in software engineering, they are structured best practices that the programmer can use to solve common problems when developing an application or system.


# Creational Patterns
### Prototype
Used to specifically to clone an attribute of an object into new object.
> Note: ES6 has introduced Classes, which is a syntactic sugar over the existing prototype pattern

```sh
function Hello (greeting) {
  this.greeting = greeting || 'Hello World!'; 
}
Hello.prototype.speak = function(somethingElse) { 
  var message = somethingElse || this.greeting;
  console.log(message); 
}

var hi = new Hello('Just saying hi!');
hi.speak();
hi.speak('Something different');

```
### Module
This is the most commonly used pattern after prototype. Module should be Immediately-Invoked-Function-Expressions (IIFE). All the modules exists within a closure.

> Note: Module is helpful when the global namespace is not polluted and keeps your function importable and exportable

```sh
var options = {
  username: 'blah',
  server: '127.0.0.1'
};
var ConfigObject = (function(params) {
  var username = params.username || '',
      server = params.server || '',
      password = params.password || '';
      function _checkPassword() {
        if (this.password === '') {
          console.log('no password!');
          return false;
        }
        return true;
      }
      function _checkUsername() {
        if (this.username === '') {
          console.log('no username!');
          return false;
        }
        return true;
      }
      function login() {
        if (_checkPassword() && _checkUsername()) {
          // perform login
        }
      }
  return {
    login: login
  }
})(options);

```

### Singleton
This should be a self-invoking, it will execute and store the instance at the time of definition.
>Note: This is used when you only ever want exactly ONE instance of an object.

```sh
var GlobalConfigurationObject = (function() {
  var instance; 
  function createInstance() {
    return new ConfigObject();
  };

  var getInstance = function() {
    if (!instance) {
      instance = createInstance();
    }
    return instance;
  }

  return {
    getInstance: getInstance
  }
})();

```
# Behavioral Patterns
### Observer
This is a subscription model, where you assign your objects to listen to events.  If you are executing a function when the event has been fired
>Note: This helps prevent highly coupled code
