# Task Runner Starter - Grunt
 
Create a lib folder

cd into the lib folder

## Start From Scratch
**`npm init`** - walk through the steps for creating a basic package.json file

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

**Common packages for projects include:**
* `npm install grunt --save-dev`
* `npm install jshint --save-dev`
* `npm install grunt-contrib-jshint --save-dev`
* `npm install jshint-stylish --save-dev`
* `npm install grunt-contrib-watch --save-dev`
* `npm install matchdep --save-dev`
* `npm install copy --save-dev`
* `npm install grunt-contrib-copy --save-dev`
* `npm install sass --save-dev`
* `npm install grunt-contrib-sass --save-dev`
* `npm install jquery --save-dev`
* `npm install bootstrap --save-dev`
* `npm install angular --save-dev`
* `npm install angular-route --save-dev`
* `npm install angularfire --save-dev`
* `npm install firebase --save-dev`

After each install - your package.json file will update

The grunt install will create a node_modules folder. This will become the location for the other items installed.

**Setup Your Gruntfile.js**

* Setup jshint - location of javascript files
* Setup sass compilation - location of scss and where to put compiled version.
* Setup watch - have grunt run specific tasks when changes occur.

### Sample Gruntfile.js
```javascript

module.exports = function(grunt) {

  grunt.initConfig({
    jshint: {
      options: {
        predef: [ "document", "console", "$", "$scope" ],
        esnext: true,
        globalstrict: true,
        globals: {"angular": true, "app": true}
      },
      files: ['../app/**/*.js']
    },
    copy: { //for bootstrap and jquery - only need to do the first time.
      bootstrap: {
        expand: true,
        cwd: 'node_modules/bootstrap/dist',
        src: ['**'],
        dest: '../dist'
      },
      jquery: {
        expand: true,
        cwd: 'node_modules/jquery/dist',
        src: ['jquery.min.js'],
        dest: '../dist'
      }
    },
    sass: {
      dist: {
        files: {
          '../css/main.css': '../sass/main.scss'
        }
      }
    },
    watch: {
      javascripts: {
        files: ['../app/**/*.js'],
        tasks: ['jshint']
      },
      sass: {
        files: ['../sass/**/*.scss'],
        tasks: ['sass']
      }
    }
  });

  require('matchdep').filterDev('grunt-*').forEach(grunt.loadNpmTasks);

  grunt.registerTask('default', ['copy', 'jshint', 'sass', 'watch']);
};



```
## Start From boilerplate
Already have a package.json file and Gruntfile.js
* Run `npm install` - this looks at the package.json file and installs the needed items.
* Run `grunt`


***********************
So, what's up with `"use strict"`
* Disallows global variables. (Catches missing var declarations and typos in variable names)
* Silent failing assignments will throw error in strict mode (assigning NaN = 5;)
* Attempts to delete undeletable properties will throw (delete Object.prototype)
* Requires all property names in an object literal to be unique (var x = {x1: "1", x1: "2"})
* Function parameter names must be unique (function sum (x, x) {...}) 
* Some ES6 features require you to be in strict mode
  
