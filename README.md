# eslint-intro
Introduction to installing and using ESLint

## Linters
A _linter_ is a tool that checks your source code to find programming errors, bugs, stylistic errors, and suspicious constructs. It can warn you of any errors or potential errors before you upload your code, or even while you're still writing it.

There are several linters available for JavaScript, and ESLint is the most popular. We will learn to install and use it, and to configure it for our own preferences.

## Prerequisites
 * VSCode, node and npm installed

## Setup
 Fork and checkout this repo https://github.com/dans-mad/eslint-intro/
 
 In the `eslint-intro` directory that you just checked out, run the following commands:
 * To set up eslint-intro as a node project, run: `npm init -y`
 * To install ESLint and its dependencies, run: `npm import --save-dev eslint eslint-config-standard eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard`
 * To create a basic configuration for linting, create a file called `.eslintrc.js` (don't forget the dot at the start!)
 * Inside that file, add: `module.exports = { "extends": "standard" };`
 * In VSCode, click on the _Extensions_ icon on the left (or hit `Ctrl+Shift+X`), search for _ESLint_, and install the ESLint plugin (it should be the first one in the list of results)

## Exercises
### Exercise 1 - identifying errors
 * Open the file `index.js`
 * Add two empty lines to the file
 * If you have ESLint and the VSCode plugin working correctly, you should see a wiggly red line
 * Hover over the wiggly red line, and a message will pop up: *Too many blank lines at the beginning of file. Max of 1 allowed.eslint(no-multiple-empty-lines)*
 * Delete all of the new lines, and replace them with the following JavaScript: `var name = 'bob'`
 * You should now see two wiggly red lines. Hover over the one under `name` and you will see _'name' is assigned a value but never used.eslint(no-unused-vars)_ 
 * Hover over the other wiggly line and you will see _Newline required at end of file but not found. eslint(eol-last)_
 * At the end of the line is a light-blue lightbulb. Click on it.
 * You will see several options. Click the top one, _Fix this eol-last problem_
 * ESLint will fix the problem for you by adding an extra line at the end of the file


### Exercise 2 - configuration
ESLint is configured using the file `eslint.rc.js`. You can use existing rule sets, add your own rules and exceptions, and combine multiple sets of rules. At the moment, our `eslint.rc.js` just does one thing: extend (i.e. inherit) the standard set of rules. Let's add some exceptions...

The full list of linting rules is at https://eslint.org/docs/rules/
The full guide for configuring ESLint is at https://eslint.org/docs/user-guide/configuring

* Replace the contents of `index.js` with this code: `var first_name = 'bob'`
* Hover over the wiggly line under `first_name` and you will see two errors. The previous one *'first_name' is assigned a value but never used.eslint(no-unused-vars)* as well as a new error *Identifier 'first_name' is not in camel case.eslint(camelcase)*
* Add a new line add the end of the file: `console.log(first_name)`
* Hover over the wiggly line again and you'll see there's now only one error. At the end of the error description it says *eslint(camelcase)*. This - _camelcase_ is the name of the rule that caught this error. Camel Case is the usual way of naming variables in JavaScript, it looks like this: `myVariableName`. But if you want variables named like this: `my_variable_name` then you will have to turn this rule off. 
* Open up `eslint.rc.js` and inside the curly brackets, after `extends: 'standard'` add a comma and then `"rules": { "camelcase": "off" }`. The whole line should read:
```
module.exports = { extends: 'standard', "rules": { "camelcase": "warn" } };
```
* Looking again at `index.js`, you will see that there are no longer any errors.
* Change `eslint.rc.js` so that instead of `"camelcase": "off"` it says `"camelcase": "warn"`
* Return to `index.js` and you'll see that the wiggly line is back, but this time it's yellow. A warning means something like _this is really not recommended, but if you're *absolutely* sure this is the best way to do it, then go ahead._

 ### Exercise 4 - npm projects
 So far, we have created the npm project for `eslint-intro` from scratch. We did this by running:
  1. `npm init -y` to initialise the project - this creates the file `package.json` and allows you to import npm modules
  2. `npm import --save-dev eslint eslint-config-standard eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard` - this does two things:
    - imports and installs the packages `eslint eslint-config-standard eslint-plugin-import eslint-plugin-node eslint-plugin-promise` and `eslint-plugin-standard` into your `node_modules` directory
    - adds these packages to the `dev-dependencies` of `package.json`.

  When you clone a git repository which is already an npm project, you do not need to initialise it. Nor do you need to add any packages to the `dev-dependencies` of `package.json`. But you _do_ need to import and install those packages. You do this by running `npm install`

  * Run `npm init` (_without the `-y`) to see what questions npm asks you when setting up a new project. Use any answers you like, and then look in `package.json` to see how it stores your answers.
  * Revert any changes you have made 
  * Now out the branch named `setup` by running`git checkout setup`
  * Open `package.json`
  * Look at the section named `devDependencies`, and see that all of the eslint packages you previously added are in there
  * Each package also lists the version of that package. In front of each of them is a carat (`^`). Investigate what this means and what other version options can be specified at https://docs.npmjs.com/files/package.json#dependencies
  * Run `npm install`
  * You will see that a new file - `package-lock.json` appears. Have a quick peek at this file (it will be very long!) It lists the _exact_ version of each package dependency, and that dependency's dependencies, and those dependencies dependencies dependencies...When working on a project with other people, you should commit `package-lock.json` to your git repo to ensure that everyone is using the _exact_ same versions of each package
  * Commit `package-lock.json` to the git repo.
  * To update any of your dependencies to the latest compatible version, run `npm update`. As you have very recently run `npm install` you will probably not get any newer versions of packages, but if and when you do then `package-lock.json` will update to show the installed version, and (assuming everything still works!) you should commit the updated `package-lock.json`

 ### Additional Exercise
  * Replace the contents of `index.js` with some of your own code, typed or pasted in. For example, you could paste your solutions to previous JavaScript exercises. See what potential problems the linter highlights, and how you can either fix them, or turn off the rules that caused them. Before you do this though, try to understand why you might want to use this rule.
  * Investigate the _prettier_ npm package: https://prettier.io/ - Prettier is not a Linter, it doesn't check or fix errors, but it rewrites your code into a standardised format (i.e. it applies rules about newlines, spacing, placing of braces and brackets etc, and formats your code to meet those rules).

## Revision
Have a look through the full list of linting rules at https://eslint.org/docs/rules/ - you don't need to learn all of these (!) but it's useful to get an idea of how they're grouped, and what types of things are covered.
You can also disable rules for individual files and blocks of code - see https://eslint.org/docs/user-guide/configuring#disabling-rules-with-inline-comments
The full guide for configuring ESLint is at https://eslint.org/docs/user-guide/configuring
