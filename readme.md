# jsonmap

[![NPM](https://nodei.co/npm/jsonmap.png?global=true)](https://nodei.co/npm/jsonmap/)

streaming command line newline-delimited json transformer utility

you must pipe newline-delimited JSON data in (one JSON stringified object per line). you will receive the same format out

## installation

```BASH
$ npm install jsonmap -g
```

## usage

`this` will be each line of JSON that gets parsed out of the incoming newline-delimited json stream

there are two 'modes', the first is where you modify `this`:

```BASH
$ echo '{"foo": "bar"}\n{"baz": "taco"}' | jsonmap "this.pizza = 1"
{"foo":"bar","pizza":1}
{"baz":"taco","pizza":1}
```

the second mode is where you return a new object:

```BASH
$ echo '{"foo": "bar", "cat": "yes"}\n{"baz": "taco", "cat": "yes"}' | jsonmap "{cat: this.cat}"
{"cat":"yes"}
{"cat":"yes"}
```

if your code gets too complex and you'd rather use an external file you can also just specify a module to get required:

```BASH
$ echo '{"foo": "bar"}\n{"baz": "taco"}' | jsonmap --file=transform.js
{"foo":"bar","pizza":1}
{"baz":"taco","pizza":1}
```

the above will work if `transform.js` has the following contents:

```js
module.exports = function() {
  this.pizza = 1
}
```
