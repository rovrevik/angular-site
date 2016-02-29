Website Application
===================

- Create the project directory.
- Initialize the directory for git and for using git-flow.
  ```bash
  git init
  git-flow init
  ```

- Create this README.
- Install the latest version of Node.js if necessary.
  ```bash
  nvm --version
  nvm install 4.3.1
  nvm alias default 4.3.1
  ```

- Upgrade npm if necessary.
  ```bash
  npm install --global npm@latest
  ```

- Create a .nvmrc file in the directory of the new project.
 *nvm does not support evaluating this when changing into the directory.*
- Install global npm packages if necessary.
  ```bash
  npm install -g bower # The browser package manager
  npm install -g grunt-cli # The grunt command line interface.
  npm install -g grunt-init # Project Scaffolding with Grunt
  npm install -g gulp # The streaming build system
  npm install -g yo # CLI tool for running Yeoman generators
  npm install -g generator-angular # Yeoman generator for AngularJS
  npm install -g generator-karma # Yeoman generator for Karma
  npm install -g generator-protractor # Yeoman generator for Protractor
  ```

### npm module installation warnings
  - grunt-init
  ```
  npm WARN deprecated lodash@0.9.2: Grunt needs your help! See https://github.com/gruntjs/grunt/issues/1403.
  npm WARN deprecated graceful-fs@1.2.3: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
  ```

  - gulp
  ```
  npm WARN deprecated graceful-fs@3.0.8: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
  npm WARN deprecated lodash@1.0.2: lodash@<3.0.0 is no longer maintained. Upgrade to lodash@^4.0.0.
  npm WARN deprecated graceful-fs@1.2.3: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
  ```

  - yo
  ```
  npm WARN deprecated npmconf@2.1.2: this package has been reintegrated into npm and is now out of date with respect to npm
  ```

  - generator-angular
  ```
  npm WARN deprecated graceful-fs@2.0.3: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
  npm WARN deprecated CSSselect@0.4.1: the module is now available as 'css-select'
  npm WARN deprecated CSSwhat@0.4.7: the module is now available as 'css-what'
  npm WARN deprecated graceful-fs@3.0.8: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
  npm WARN deprecated lodash@2.1.0: lodash@<3.0.0 is no longer maintained. Upgrade to lodash@^4.0.0.npm WARN generator-angular@0.15.1 requires a peer of generator-karma@>=0.9.0 but none was installed.
  ```

  - generator-karma
  ```
  npm WARN deprecated native-or-bluebird@1.2.0: please use 'any-promise' instead
  ```

## Generate the application scaffolding.
```bash
yo angular site
```

Stick with the defaults for the most part.

- Use Grunt instead of Gulp.
- Don't use Sass (with Compass)
- Include Bootstrap
- AngularJS modules included
    - angular-animate.js
    - angular-cookies.js
    - angular-resource.js
    - angular-route.js
    - angular-sanitize.js
    - angular-touch.js
- AngularJS modules excluded
    - angular-aria.js
    - angular-messages.js
- Overwrite README.md

### Update bower.json to use tilde version ranges for angular and bootstrap.
- "angular": "^1.4.0" will pull down 1.5.0
- Only allow patch-level changes.
- Use the highest Angular 1.4 version available instead of the highest version over 1.4. `^1.4.0` changed to `~1.4.0`
- Use the highest Bootstrap 3.2 version available instead of the highest version over 3.2. `^3.2.0` changed to `~3.2.0`

## Set up e2e testing with the Yeoman Protractor Generator
- [e2e Testing](https://code.angularjs.org/1.5.0/docs/guide/e2e-testing)
```bash
npm install -g generator-protractor
yo protractor
```

Stick with the defaults.
The generator overwrites the package.json so it needs to be manually merged.
Add e2e entries for the scripts section of the package.json file.
```json
"scripts": {
  "webdriver": "webdriver-manager start",
  "protractor": "protractor protractor.conf.js"
}
```

Add directConnect: true to the protractor config file so that a selenium server doesn't need to be running.
https://github.com/angular/protractor/blob/master/docs/server-setup.md

### Colocate e2e Protractor test support with the unit test support created by the Yeoman AngularJS generator.
The existing test directory was created by the Yeoman AngularJS generator.
Move protractor.conf.js and README.txt from the project root directory into the test directory.
Change paths for moved protractor files.
Rename protractor spec directory to e2e-spec.
Move the example protractor e2e-spec directory from the project directory into the test directory.
Add test/e2e-spec patterns to Gruntfile for jshint and jscs.
Rework watch to separate tasks for checking all tests but only executing karma for unit test.
Add jshint configuration for protractor. https://github.com/angular/protractor/blob/master/spec/.jshintrc

## Add UI Bootstrap/angular-bootstrap
[angular-bootstrap](https://github.com/angular-ui/bootstrap-bower) is a bower repository to hold Angular UI Bootstrap releases
[angular-ui-bootstrap-bower](https:github.com/angular-ui/bootstrap-bower) is a bower repository to hold Angular UI Bootstrap releases.
[angular-ui-bootstrap](https:github.com/angular-ui/bootstrap.git) Note: do not install 'angular-ui-bootstrap'.
```bash
bower install angular-bootstrap --save
```
Add UI Bootstrap/angular-bootstrap with `bower install angular-bootstrap --save`
Execute `grunt wiredep` to add ui-bootstrap in the required files.
Add an example for using ui-bootstrap. http://angular-ui.github.io/bootstrap/#buttons

[AngularUI](https://angular-ui.github.io/)

## Add Font Awesome
Add font awesome with `bower install font-awesome --save`
Add font-awesome override to bower.json to keep wiredep from removing the include.
Execute `grunt wiredep` to add font-awesome in the required files.
Add an example for using font awesome. [Basic Icons](https://fortawesome.github.io/Font-Awesome/examples/#basic)

## Documentation and Reference
- [Node.js](https://nodejs.org/en/docs/)
- [npm](https://docs.npmjs.com/)
- [Bower](http://bower.io/)
- [GRUNT](http://gruntjs.com/getting-started)
- [Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
- [Yeoman](http://yeoman.io/learning/)
- [AngularJS generator](https://github.com/yeoman/generator-angular)
- [Karma generator](https://github.com/yeoman/generator-karma)
- [Protractor generator](https://github.com/andresdominguez/generator-protractor)
- [Karma](http://karma-runner.github.io/)
- [PhantomJS](http://phantomjs.org/documentation/)
- [Jasmine](http://jasmine.github.io/2.4/introduction.html)
- [Protractor](http://www.protractortest.org/#/)
- [grunt-contrib-watch](https://github.com/gruntjs/grunt-contrib-watch)
- [JSHint](http://jshint.com/docs/)
- [JSCS](http://jscs.info/overview)

- [AngularJS](https://docs.angularjs.org/guide)
- [UI Bootstrap](https://angular-ui.github.io/bootstrap/)
- [Font Awesome](https://fortawesome.github.io/Font-Awesome/)

- [nvm](https://github.com/creationix/nvm) (Node Version Manager)
- [n](https://github.com/tj/n)
- [Autoenv](https://github.com/kennethreitz/autoenv)
- [avn](https://github.com/wbyoung/avn) (Automatic Version Switching for Node)
