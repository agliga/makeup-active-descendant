# makeup-active-descendant

<p>
    <a href="https://travis-ci.org/makeup-js/makeup-active-descendant"><img src="https://api.travis-ci.org/makeup-js/makeup-active-descendant.svg?branch=master" alt="Build Status" /></a>
    <a href='https://coveralls.io/github/makeup-js/makeup-active-descendant?branch=master'><img src='https://coveralls.io/repos/makeup-js/makeup-active-descendant/badge.svg?branch=master&service=github' alt='Coverage Status' /></a>
    <a href="https://david-dm.org/makeup-js/makeup-active-descendant"><img src="https://david-dm.org/makeup-js/makeup-active-descendant.svg" alt="Dependency status" /></a>
    <a href="https://david-dm.org/makeup-js/makeup-active-descendant#info=devDependencies"><img src="https://david-dm.org/makeup-js/makeup-active-descendant/dev-status.svg" alt="devDependency status" /></a>
</p>

Implements ARIA <a href="https://www.w3.org/WAI/GL/wiki/Using_aria-activedescendant_to_allow_changes_in_focus_within_widgets_to_be_communicated_to_Assistive_Technology">active descendant</a> keyboard navigation.

A vanilla JavaScript port of <a href="https://github.com/ianmcburnie/jquery-active-descendant">jquery-active-descendant</a>.

## Experimental

This module is still in an experimental state, until it reaches v1.0.0 you must consider all minor releases as breaking changes. Patch releases may introduce new features, but will be backwards compatible.

## Install

```js
// via npm
npm install makeup-active-descendant

// via yarn
yarn add makeup-active-descendant
```

## Example

```js
// require the module
const ActiveDescendant = require('makeup-active-descendant');

// get the widget root element reference
const widgetEl = document.querySelector('.widget');

// get the focus element reference
const focusEl = widgetEl.querySelector('input');

// get the owned element reference
const ownedEl = widgetEl.querySelector('ul');

// create an activeDescendant widget instance on the element
const activeDescendant = ActiveDescendant.createLinear(widgetEl, focusEl, ownedEl, 'li');

// listen for events (optional)
widgetEl.addEventListener('activeDescendantChange', function(e) {
    console.log(e.detail);
});
```

Markup before:

```html
<div class="widget">
    <input type="text">
    <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ul>
</div>
```

Markup after instantiation:

```html
<div class="widget" id="widget-0">
    <input type="text" aria-owns="widget-0-list-0">
    <ul id="widget-0-list-0">
        <li id="widget-0-item-0" data-makeup-index="0">Item 1</li>
        <li id="widget-0-item-1" data-makeup-index="1">Item 2</li>
        <li id="widget-0-item-2" data-makeup-index="2">Item 3</li>
    </ul>
</div>
```

Markup after pressing down arrow key on focusable element:

```html
<div class="widget" id="widget-0">
    <input type="text" aria-activedescendant="widget-0-item-0" aria-owns="widget-0-list-0">
    <ul id="widget-0-list-0">
        <li class="active-descendant" id="widget-0-item-0" data-makeup-index="0">Item 1</li>
        <li id="widget-0-item-1" data-makeup-index="1">Item 2</li>
        <li id="widget-0-item-2" data-makeup-index="2">Item 3</li>
    </ul>
</div>
```

Use CSS to style the active descendant however you wish:

```css
.widget .active-descendant {
    font-weight: bold;
}
```

## Options

* `activeDescendantClassName`: the HTML class name that will be applied to the ARIA active descendant element (default: 'active-descendant')

## Custom Events        

* `activeDescendantChange`
    * detail
        * fromIndex
        * toIndex

## Dependencies

* `makeup-navigation-emitter`
* `makeup-next-id`

## Development

* `npm start`
* `npm test`
* `npm run lint`
* `npm run fix`
* `npm run build`
* `npm run clean`

The following hooks exist, and do not need to be invoked manually:

* `npm prepublishOnly` cleans, lints, tests and builds on every `npm publish` command
* `pre-commit` cleans, lints, tests and builds on every `git commit` command

## Test Reports

Each test run will generate the following reports:

* `/reports/coverage` contains Istanbul code coverage report
* `/reports/html` contains HTML test report

## CI Build

https://travis-ci.org/makeup-js/makeup-active-descendant

## Code Coverage

https://coveralls.io/github/makeup-js/makeup-active-descendant