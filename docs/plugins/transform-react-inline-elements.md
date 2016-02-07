---
layout: docs
title: React inline elements transform
description:
permalink: /docs/plugins/transform-react-inline-elements/
package: babel-plugin-transform-react-inline-elements
---

Create JSX elements more quickly by using a stripped-down helper function instead of calls to `React.createElement`. This [skips a loop through props](https://github.com/babel/babel/pull/2972#issue-116267142) which leads to improved performance.

Careful with this optimization! If you use a Symbol polyfill, be sure to make it global and export the global before importing React. If you don't, this optimization [will break on older browsers](https://github.com/facebook/react/issues/5138#issue-110986133).

This transform **should be enabled only in production** (e.g., just before minifying your code) because although they improve runtime performance, they make warning messages more cryptic and skip important checks that happen in development mode, including propTypes.

## Example

**In**

```javascript
<Baz foo="bar"></Baz>;
```

**Out**

```javascript
babelHelpers.jsx(Baz, {
  foo: "bar"
});
```

## Installation

```sh
$ npm install babel-plugin-transform-react-inline-elements
```

## Usage

Add the following line to your `.babelrc`:

```json
{
  "plugins": ["transform-react-inline-elements"]
}
``
