Slides: http://yom.nu/ngstrangeloop-slides

- Lukas Ruebbelke @simpulton; coauthor angularjs in action

- matias niemela @yearofmoo; angularjs contributor

- joel hooks @jhooks; egghead.io Partner


# History

developed in 2009 by misko hevery
released in 2010 at 0.9.0

# Elevator Pitch

 - intuitive framework, easy to organize code
 - prescriptive, not too restrictive
 - written to be testable
 - 2-way data binding saves 100s of lines of code
 - templates are html
 - data structures are just javascript, simplifying integration
 - 99 problems but scope ain't one

# Demo

 - see the slide called "Basic (Demo) AngularJS Application" for instructions

## How it works

 - ng-app "starts" the application
   - angular.module('myApp', []....
     - the empty brackets are dependencies to other modules
 - "directive" is reusable html component
   - that directive can be used wherever you need it
   - operations that are outside of angular's lifecycle require you to use $scope.$apply(...). See apply.html for details

 - $compile() is part of angular's dependency injection system
   - it's an angular service
   - it'll compile down the templates / bindings ({{ num }}), for example
     - it grabs all the html chunks and then binds it to $scope
 - $digest
   - a bit more internal
   - similar to $apply

 - the directive has a controller, a template, links, templateUrl, etc



### From scratch

 - Note: this is not correct html/javascript. missing brackets and such... me fast typing

 ```
 <html ng-app='app'>
   <body ng-init="name='John'">
   {{ name }}

   <button ng-click="name='Ian'">Change it</button>

   </body>

   <script ... angular ></script>
   <script>
    angular.module('app',[]) // for this to work, requires ng-app='app' in the html element
    .directive('changeName', function(){
     return function($scope, element, attrs) {
       element.bind('click', function() {
         // without $apply, this will not work!
         $scope.$apply(....){
           $scope.name = 'Paul';
         });
         }
         });
   </script>
 </html>
 ```

 - ng-click is an angular reusable event

 - these modules **can** become huge and monolithic, but angular supports submodules and that's the direction you want to go

 - ng-app can get attached to other elements (NOT head!)
   - you could make just a single div an angular js application, for example
   - you can make widgets, essentially
   - you can bring angular widgets into legacy apps, for example
   - ng-apps can be included in other ng-apps, such that you can reuse entire apps


### Recap

  - "Hello AngularJS from scratch" slide

 //script.js
  - 1. define module (angular.module('myApp'...)
     .controller()

 //index.html
  - 2. <html ng-app="myApp">

  - 3. <body ng-controller="MainCtrl">
       <h1>Hello {{world}}</h1>
       </body>


  - Note how Lucas's example is much different from Matias's simple example (i.e. it uses a controller)


 - Follow the 80/20 rule
   - you can get 80% of what you need done with straight up angular

# Build a strong angularjs foundation

## Big Picture

  - "Module" at the top: <html ng-app="modulename">
  - "Config"
  - "Routes"
  - "View" and "Controller" glued together with $scope
  - Directives to extend views
  - Services to supplement controllers

## Compile
   - compiles dom into template, links it with scope
   - "zipper" is a good metaphor for what's going on here

## Digest and apply
   - $digest processes all watchers of the current scope
   - $apply() is used to notify that something has happened outside of the angularjs domain
   - $apply() forces a $digest cycle
   - $digest is built around dirty checking
   - generally, you use $apply() which has error handling mechanisms built into it
   - rarely ever call $digest

   - Since the page updates on a apply/digest cycle, how does this actually happen?
     - is it on a loop?

   - No.

   - $rootScope is the big mama
     - everything inherits from it
   - you can get higher performance by using child scopes
     - more on that later, apparently


## Module View Whatever
   - choose the Whatever that works for you

   - Lukas likes MVVM

## Controller and $scope

  - $scope glue between Controller and View
  - Controller responsible for constructing the model on $scope and providing commands for the View to act upon
  - $scope provides context
  - inside a loop, for example, each iteration creates a child scope, such that scope doesn't leak

  - Controller: imperative behavior
  - Scope: Glue
  - View (DOM): declarative view

  - by separating imperative behavior from view, behavior becomes much easier to test
  - View is AngularJS compiled DOM
  - DOM is no longer single source of truth
  - View is the product of $compile merging the HTML template with $scope


## Models and Services

   - Services carry out common tasks specific to the web app
   - services are consumed via dependency injection
   - services are application singletons
   - services are instantiated lazily

   - !! Holy hell.... this feels SO much like Flex and swiz, or even a typical MVC with DI on the backend


## Routes
  - $route deep links URLs to controllers and views
  - include the ngRoute module into your code
  - Define routes using $routeProvider
  - typically used in conjunction with ngView directive and $routeParams service


# More Demo
   - app.js
     - notice how it includes other modules
     - "ngXYZ" are core angular modules
     - note the .run() function
   - config.js
     - .constant('SOME_THING', 'some_value')
     - .run() includes a partial function

   - He likens this DI system to the Spring xml file

   - firebase.js
     - this is a separate module
     - why is he including  redundant dependencies?
       - so that each module can stand alone

   - helpers.js
    - includes filters via .filter(), and other stuff via .factory()

   - index.html

     - note the "ng-view" div... this is where the view gets placed that gets sucked in
     - all those scripts could be included with grunt, but he included them independently for clarity

   - homePages.js
    - angular.module(..)
    - $routeProvider
      - includes the home.html page


# Testing
   - for functional tests, moving to a thing called "protractor" which uses selenium
   - will be in angularjs 1.2

   - unit tests

    - uses Karma
    - tell Karma whether to use jasmine or mocha
    - tell it what browsers to run against
    - in Gruntfile.js, configure all the things, such as autotest, etc
    - karma-unit.conf.js for other configs
    - see package.json for all the required node modules
    - karma has an 'output' for junit xml

    - protractor
      - uses selenium jar file
      - gives matchers and specific events to test the app
      - see homeSpec.js in his code


# Directives

## Simplified World View

  - most directives consist of 3 things or less
  - firm grasp on these will make advanced directives more approachable
  - directives can be one of the most complicated things in angular
   - so it's essential to have a firm foundation


 - Directive Definition Object (DDO)
  - tells compilar how a directive should be assembled
  - common properties are link function, controller function, restrict, remplate, and template Url
    - tangent: if you concat files using grunt or require, you can compile those templates into strings and use template instead of templateUrl

 - Controller function
  - controler constructed during pre-linking phase
  - receives $scope which is the current scope for the element

 - Link function
  - where DOM manipulation happens
  - comes with scope, element, and attrs
  - scope is the same $scope in the controller function
  - is a jq-like instance of the DOM element the directive is declared in
  - attrs is a list of attributes declared on the element
  
 - apply.html
  - see angular.module().directive(....) for example
  - that thing being returned is the link function
  - note how you don't have to do any kind of dom manipulation (lookups, etc)
  - later on, notice the 'templateExample' where it returns an object with a controller, template, link function
  - even later, 'templateUrlExample' shows how to use a templateUrl
    - note in this example, it doesn't refer to a file but refers to a ng-template defined in a javascript block
    
    - script type="text/ng-template" id="click-template"...
      - html goes here
      
  - you don't want to modify scope data inside of a controller, not directly in the directive
  
# Server-side integration with Angular JS

 - $HTTP
   - $http service via xmlhttpservice or jsonp
   - based on deferred / promises APIs, exposed by $q service
   - var deferred - $q.defer(), for example
   - $http.get(url).success(deferred.resolve).error(deferred.reject)
   - return deferred.promise

 - $HTTP shortcut methods
   - see slides, eg. $get, $post, $jsonp

 - Promises
  - returned value of $http is a promise
  - use `then` method to register callbacks
  - callbacks receive a single arg - the object representing the response

# Real Time Communication

 - git checkout  step_2

 - Firebase demo

 - listPages.js
   - angular.module()...
   - note the use of 'resolve' inside the when() functions
    - this ulatimately results in new data being injected via DI, i.e. the 'lists' variable

 - show.html
  - Whoa... the databinding is  slick
    - updating in the edit text field real-time updates it in the nav sidebar
    - All of this is due to $scope
    - All of this happens via the different attributes on the form tag
      - ng-change, eg
    - has to use $parent because it's inside an ng-repeat, and so the parent refers to the controller


 - Validations
  - you can do html validations
  - listPages.js
  - in submit function, checks for listForm.$valid
  - but that's generally all you do in the controller... validation happens in the template

  - form.html
   - ng-model assigns an input field to $scope
   - add 'required' as html5 validation attribute; angular will automatically hook into it

 - Animations
  - uses CSS
  - see ng-enter, ng-leave, etc in the animations.css

# Testing, again

 - karma is the current test runner
 - Protractor is next-gen scenario runner
 - Karma is testing framework agnostic
 - easiest way to get up and running with Karma and testing in general is with Yeoman
  - it generates the test environment for you
  - it can generate controllers as well as test stuff
  - but easy isn't always better
  - so probably it's OK to start with it to get a feel for it, but probably not something you do in a real app


## Unit Testing

 - test isolated pieces or units of logic
 - matchers, mocks, and/or spies

### Matchers

 - actual/expected
 - expect(a).toBe(b)

### Mocks

 - use Angular to mock out specific areas of code
 - see his slide for example
 - angularjs test code uses a ton of this
 - mathias recommends using mocks over spies when possible because the DI system ties into the mocking system cleanly

## End to end testing

 - Protractor
  - not yet ready
 - controller tests
  - note how he overrides methods on javascript variables, i.e. lists.remove() = function... This is what injectMethod does in mxunit. So: simple mocking

  - debugger;
   - put this in your test code
   - will enable you to interact with this using chrome's debugger
   - just click the "DEBUG" button on the web page

 - Grunt
  - Gruntfile.js
  - load grunt karma plugin (see example)
  - in the karma:{} block, specify config