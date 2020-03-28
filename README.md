# eslint-intro
Introduction to installing and using ESLint

A _linter_ is a tool that checks your source code to find programming errors, bugs, stylistic errors, and suspicious constructs.

There are several linters available for JavaScript, and ESLint is the most popular. You can configure it using  

## prerequisites
 * node and npm installed

## Setup
 In the `eslint-intro` directory, run the following commands:
 * To set up eslint-intro as a node project, run: `npm init`
 * To install ESLint and its dependencies, run: `npm i -D eslint eslint-config-standard eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard`
 * To create a basic configuration for linting, create a file called `.eslintrc.js` (don't forget the dot at the start!)
 * Inside that file, add: `module.exports = { "extends": "standard" };`
 * In VSCode, click on the _Extensions_ icon on the left (or hit `Ctrl+Shift+X`), search for _ESLint_, and install the ESLint plugin (it should be the first one in the list of results)

