# Javascript Coding Standard

*A mostly reasonable approach to JavaScript whilst working at StayNTouch*

## Index

1. [Objects](#objects)
1. [Arrays](#arrays)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Properties](#properties)
1. [Variables](#variables)
1. [Conditional Expressions & Equality](#conditional-expressions-&-equality)
1. [Blocks](#blocks)
1. [Comments](#comments)
1. [Whitespace](#whitespace)
1. [Naming Conventions](#naming-conventions)


## Objects

  - Use the literal syntax for object creation.

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

**[back to top](#index)**


## Arrays

  - Use the literal syntax for array creation.

    ```javascript
    // bad
    var item = new Array();

    // good
    var item = [];
    ```

**[back to top](#index)**


## Strings

  - Use single quotes `''` for strings

    ```javascript
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```

**[back to top](#index)**


## Functions

  - Function expressions:

    ```javascript
    // anonymous function expression
    var anonymous = function() {
      return true;
    };

    // named function expression
    var named = function named() {
      return true;
    };

    // immediately-invoked function expression (IIFE)
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead:

  	```javascript
  	// bad
  	if (currentUser) {
  	  function test() {
  	    console.log('Nope.');
  	  }
  	}

  	// good
  	var test;
  	if (currentUser) {
  	  test = function test() {
  	    console.log('Yup.');
  	  };
  	}
  	```

**[back to top](#index)**


## Properties

  - few goods and bads

    ```javascript
    // bad
    var isJedi = luke['jedi'];

    // good
    var isJedi = luke.jedi;

    // good
    var prop = 'jedi';
    var isJedi = luke[prop];
    ```

**[back to top](#index)**


## Variables

  - Always use `var` to declare variables. Not doing so will result in global variables..

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - Use one var declaration for multiple variables and declare each variable on a newline.

  	```javascript
    // bad
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';
    ```

  - Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

  	```javascript
  	// bad
  	var i, len, dragonball,
  	    items = getItems(),
  	    goSportsTeam = true;

  	// bad
  	var i, items = getItems(),
  	    dragonball,
  	    goSportsTeam = true,
  	    len;

  	// good
  	var items = getItems(),
  	    goSportsTeam = true,
  	    dragonball,
  	    length,
  	    i;
  	```

  - Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

  	```javascript
  	// bad
  	function() {
  	  test();
  	  console.log('doing stuff..');

  	  //..other stuff..

  	  var name = getName();

  	  if (name === 'test') {
  	    return false;
  	  }

  	  return name;
  	}

  	// good
  	function() {
  	  var name = getName();

  	  test();
  	  console.log('doing stuff..');

  	  //..other stuff..

  	  if (name === 'test') {
  	    return false;
  	  }

  	  return name;
  	}

  	// bad
  	function() {
  	  var name = getName();

  	  if (!arguments.length) {
  	    return false;
  	  }

  	  return true;
  	}

  	// good
  	function() {
  	  if (!arguments.length) {
  	    return false;
  	  }

  	  var name = getName();

  	  return true;
  	}
  	```

**[back to top](#index)**


## Conditional Expressions & Equality

  - Use `===` and `!==` over `==` and `!=`.

  - Conditional expressions are evaluated using coercion with the `ToBoolean` method and always follow these simple rules:

    	+ **Objects** evaluate to **true**
        + **Undefined** evaluates to **false**
        + **Null** evaluates to **false**
        + **Booleans** evaluate to **the value of the boolean**
        + **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
        + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

**[back to top](#index)**


## Blocks

  - Use braces with all multi-line blocks.

  - Conditional expressions are evaluated using coercion with the `ToBoolean` method and always follow these simple rules:

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function() { return false; }

    // good
    function() {
      return false;
    }
    ```

**[back to top](#index)**


## Comments

  - Use `/** ... */` for multiline comments. Include a description, specify types and values for all parameters and return values.

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param <String> tag
    // @return <Element> element
    function make(tag) {

      // ...stuff...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param <String> tag
     * @return <Element> element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  - Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment.

    ```javascript
    // bad
    var active = true;  // is current tab

    // good
    // is current tab
    var active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }
    ```

  - Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME -- need to figure this out` or `TODO -- need to implement`.

  - Use `// FIXME:` to annotate problems

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

  - Use `// TODO:` to annotate solutions to problems

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
  ```

**[back to top](#index)**


## Whitespace

  - Use hard tabs set to 4 spaces as with soft tabs set to 2 spaces the code looks cluttery

    ```javascript
    // bad
    function() {
    ∙var name;
    }

    // bad
    function() {
    ∙∙var name;
    }

    // good
    function() {
    ∙∙∙∙var name;
    }
    ```

  - Place 1 space before the leading brace.

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });
    ```

  - Set off operators with spaces.

    ```javascript
    // bad
    var x=y+5;

    // good
    var x = y + 5;
    ```

  - Place an empty newline at the end of the file.

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);
    ```

    ```javascript
    // good
    (function(global) {
      // ...stuff...
    })(this);

    ```

  - Use indentation when making long method chains.

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
        .attr('width',  (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // good
    var leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .class('led', true)
        .attr('width',  (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);
    ```

**[back to top](#index)**


## Naming Conventions

  - Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - Use camelCase when naming objects, functions, and instances

    ```javascript
    // bad
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    function c() {};
    var u = new user({
      name: 'Bob Parr'
    });

    // good
    var thisIsMyObject = {};
    function thisIsMyFunction() {};
    var user = new User({
      name: 'Bob Parr'
    });
    ```

  - Use PascalCase when naming constructors, classes

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    var bad = new user({
      name: 'nope'
    });

    // good
    function User(options) {
      this.name = options.name;
    }

    var good = new User({
      name: 'yup'
    });
    ```

  - Use a leading underscore `_` when naming private properties

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';

    // good
    this._firstName = 'Panda';
    ```

  - When saving a reference to `this` use `_this`. Better if you can use javascript bind() method to supply `this`. For more powerful bind use UnderscoreJS [_.bind()](http://underscorejs.org/#bind)

    ```javascript
    // bad
    function() {
      var self = this;
      return function() {
        console.log(self);
      };
    }

    // bad
    function() {
      var that = this;
      return function() {
        console.log(that);
      };
    }

    // good
    function() {
      var _this = this;
      return function() {
        console.log(_this);
      };
    }
    ```

  - Name your functions. This is helpful for stack traces.

    ```javascript
    // bad
    var log = function(msg) {
      console.log(msg);
    };

    // good
    var log = function log(msg) {
      console.log(msg);
    };
    ```

**[⬆ back to top](#index)**
