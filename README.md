# expect-webdriverio

[![Build Status](https://travis-ci.org/webdriverio/expect-webdriverio.svg?branch=master)](https://travis-ci.org/webdriverio/expect-webdriverio) [![codecov](https://codecov.io/gh/webdriverio/expect-webdriverio/branch/master/graph/badge.svg)](https://codecov.io/gh/webdriverio/expect-webdriverio)

###### [TypeScript / JS Autocomplete](/docs/Types.md) | [Examples](docs/Examples.md) | [Extending Matchers](/docs/Extend.md)

> [WebdriverIO](https://webdriver.io/) Assertion library inspired by [expect](https://www.npmjs.com/package/expect)

## Key Features

- [waits](#default-options) for expectation to succeed
- detailed [error messages](#error-messages)
- works in Mocha, Cucumber, Jest, Jasmine
- builtin [types](docs/Types.md) for TypeScript and JS autocompletion

## Installation

1. `npm install expect` (**Jasmine** and **Jest** users should skip this step)
2. `npm install expect-webdriverio`

NOTE: [WebdriverIO](https://github.com/webdriverio/webdriverio) `v5.16.11` or higher is required!

## Usage

In your `wdio.conf.js`
```js
beforeSession () { // before hook works as well
    require('expect-webdriverio')
},
```

In your test
```js
const $button = $('button')
expect($button).toBeDisplayed()
```

See more [Examples](docs/Examples.md)

## API

See available [Matchers](https://github.com/webdriverio/expect-webdriverio/blob/master/types/expect-webdriverio.d.ts#L64)

Besides of the `expect-webdriverio` matchers you can use builtin Jest's [expect](https://jestjs.io/docs/en/expect) assertions or [expect/expectAsync](https://jasmine.github.io/api/3.5/global.html#expect) for Jasmine.

## Default Options

```js
{
    wait: 2000, // ms to wait for expectation to succeed
    interval: 100, // interval between attempts
}
```

Set options like this:
```js
beforeSession () { // before hook works as well
    require('expect-webdriverio').setOptions({ wait: 5000 })
},
```

### Matcher Options

Every matcher can take several options that allows you to modify the assertion:

##### Command Options

| Name | Type | Details |
| ---- | ---- | ------- |
| <code><var>wait</var></code> | number | time in ms to wait for expectation to succeed. Default: `3000` |
| <code><var>interval</var></code> | number | interval between attempts. Default: `100` |
| <code><var>message</var></code> | string | user message to prepend before assertion error |

##### String Options

This options can be applied in addition to the command options when strings are being asserted.

| Name | Type | Details |
| ---- | ---- | ------- |
| <code><var>ignoreCase</var></code> | boolean | apply `toLowerCase` to both actual and expected values |
| <code><var>trim</var></code> | boolean | apply `trim` to actual value |
| <code><var>containing</var></code> | boolean | expect actual value to contain expected value, otherwise strict equal. |
| <code><var>asString</var></code> | boolean | might be helpful to force converting property value to string |

##### Number Options

This options can be applied in addition to the command options when numbers are being asserted.

| Name | Type | Details |
| ---- | ---- | ------- |
| <code><var>eq</var></code> | number | equals |
| <code><var>lte</var></code> | number | less then equals |
| <code><var>gte</var></code> | number | greater than or equals |

## Browser Matchers

### toHaveUrl

Checks if browser is on a specific page.

##### Usage

```js
browser.url('https://webdriver.io/')
expect(browser).toHaveUrl('https://webdriver.io')
```

### toHaveUrlContaining

Checks if browser is on a specific page and contains the given value in URL.

##### Usage

```js
browser.url('https://webdriver.io/')
expect(browser).toHaveUrlContaining('webdriver.io')
```

### toHaveTitle

Checks if website has a specific title.

##### Usage

```js
browser.url('https://webdriver.io/')
expect(browser).toHaveTitle('WebdriverIO · Next-gen browser and mobile automation test framework for Node.js')
```

### toHaveTitleContaining

Checks if website has a specific title that contains the given value.

##### Usage

```js
browser.url('https://webdriver.io/')
expect(browser).toHaveTitleContaining('Next-gen browser and mobile automation test framework')
```

## Element Matchers

### toBeDisplayed

Calls [`isDisplayed`](/docs/api/element/isDisplayed.html) on given element.

##### Usage

```js
const elem = $('#someElem')
expect(elem).toBeDisplayed()
```

### toBeVisible

Same as `toBeDisplayed`.

##### Usage

```js
const elem = $('#someElem')
expect(elem).toBeVisible()
```

### toExist

Calls [`isExisting`](/docs/api/element/isExisting.html) on given element.

##### Usage

```js
const elem = $('#someElem')
expect(elem).toExist()
```

### toBePresent

Same as `toExist`.

##### Usage

```js
const elem = $('#someElem')
expect(elem).toBePresent()
```

### toBeExisting

Same as `toExist`.

##### Usage

```js
const elem = $('#someElem')
expect(elem).toBeExisting()
```

### toBeFocused

Checks if element has focus. This assertion only works in a web context.

##### Usage

```js
const elem = $('#someElem')
expect(elem).toBeFocused()
```

### toHaveAttribute

Checks if an element has a certain attribute with a specific value.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveAttribute('class', 'form-control')
```

### toHaveAttr

Same as `toHaveAttribute`.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveAttr('class', 'form-control')
```

### toHaveAttributeContaining

Checks if an element has a certain attribute that contains a value.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveAttributeContaining('class', 'form')
```

### toHaveAttrContaining

Same as `toHaveAttributeContaining`.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveAttrContaining('class', 'form')
```

### toHaveClass

Checks if an element has a certain class name.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveClass('form-control', { message: 'Not a form control!', })
```

### toHaveClassContaining

Checks if an element has a certain class name that contains provided value.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveClassContaining('form')
```

### toHaveProperty

Checks if an element has a certain property.

##### Usage

```js
const elem = $('#elem')
expect(elem).toHaveProperty('height', 23)
expect(elem).not.toHaveProperty('height', 0)
```

### toHaveValue

Checks if an input element has a certain value.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveValue('user', { ignoreCase: true })
```

### toHaveValueContaining

Checks if an input element contains a certain value.

##### Usage

```js
const myInput = $('input')
expect(myInput).toHaveValueContaining('us')
```

### toBeClickable

Checks if an element can be clicked by calling [`isClickable`](/docs/api/element/isClickable.html) on the element.

##### Usage

```js
const elem = $('#elem')
expect(elem).toBeClickable()
```

### toBeDisabled

Checks if an element is disabled by calling [`isEnabled`](/docs/api/element/isEnabled.html) on the element.

##### Usage

```js
const elem = $('#elem')
expect(elem).toBeDisabled()
// same as
expect(elem).not.toBeEnabled()
```

### toBeEnabled

Checks if an element is enabled by calling [`isEnabled`](/docs/api/element/isEnabled.html) on the element.

##### Usage

```js
const elem = $('#elem')
expect(elem).toBeEnabled()
// same as
expect(elem).not.toBeDisabled()
```

### toBeSelected

Checks if an element is enabled by calling [`isSelected`](/docs/api/element/isSelected.html) on the element.

##### Usage

```js
const elem = $('#elem')
expect(elem).toBeSelected()
```

### toBeChecked

Same as `toBeSelected`.

##### Usage

```js
const elem = $('#elem')
expect(elem).toBeChecked()
```

### toHaveHref

Checks if link element has a specifc link target.

##### Usage

```js
const link = $('a')
expect(link).toHaveHref('https://webdriver.io')
```

### toHaveLink

Same as `toHaveHref`.

##### Usage

```js
const link = $('a')
expect(link).toHaveLink('https://webdriver.io')
```

### toHaveHrefContaining

Checks if link element contains a specifc link target.

##### Usage

```js
const link = $('a')
expect(link).toHaveHrefContaining('webdriver.io')
```

### toHaveLinkContaining

Same as `toHaveHrefContaining`.

##### Usage

```js
const link = $('a')
expect(link).toHaveLinkContaining('webdriver.io')
```

### toHaveId

Checks if element has a specific `id` attribute.

##### Usage

```js
const elem = $('#elem')
expect(elem).toHaveId('elem')
```

### toHaveText

Checks if element has a specific text.

##### Usage

```js
browser.url('https://webdriver.io/')
const elem = $('.tagline')
expect(elem).toHaveText('Next-gen browser and mobile automation test framework for Node.js')
```

### toHaveTextContaining

Checks if element contains a specific text.

##### Usage

```js
browser.url('https://webdriver.io/')
const elem = $('.tagline')
expect(elem).toHaveTextContaining('browser and mobile automation test framework')
```

### toBeDisplayedInViewport

Checks if an element is within the viewport by calling [`isDisplayedInViewport`](/docs/api/element/isDisplayedInViewport.html) on the element.

##### Usage

```js
const elem = $('#elem')
expect(elem).toBeDisplayedInViewport()
```

### toBeVisibleInViewport

Same as `toBeDisplayedInViewport`.

##### Usage

```js
const elem = $('#elem')
expect(elem).toBeVisibleInViewport()
```

### toHaveChildren

Checks amount of fetched elements using [`$$`](/docs/api/browser/$$.html) command.

##### Usage

```js
const elems = $$('div')
expect(elems).toHaveChildren({ gte: 10 })
// same as
assert.ok(elems.length >= 10)
```

### toBeElementsArrayOfSize

Same as `toHaveChildren`.

##### Usage

```js
const elems = $$('div')
expect(elems).toBeElementsArrayOfSize({ gte: 10 })
// same as
assert.ok(elems.length >= 10)
```

## Error messages

Error messages are informative out of the box and contain:

- full element selector, like `$('form').$('input')`
- actual and expected values
- highlight the difference (texts assertions)

![toHaveText](/docs/img/errors/text.png?raw=true "toHaveText")
![toHaveClass](/docs/img/errors/class.png?raw=true "toHaveClass")
![not.toBeVisible](/docs/img/errors/not-visible.png?raw=true "not.toBeVisible")

## What's next?

First of all, **feel free to raise an issue with your suggestions or help with PR!**

### Planned

- css matcher
- size matcher
- cookie / localStorage matchers?
- text regex matchers
- multiremote support (if requested)
