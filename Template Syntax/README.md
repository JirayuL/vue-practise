# Template Syntax
Vue.js uses an HTML-based template syntax that allows declaratively bind the rendered DOM to the underlying Vue instance’s data. All Vue.js templates are valid HTML that can be parsed by spec-compliant browsers and HTML parsers.

 Vue is able to intelligently figure out the minimal number of components to re-render and apply the minimal amount of DOM manipulations when the app state changes.

## Interpolations
#### Text
The most basic form of data binding is text interpolation using the “Mustache” syntax (double curly braces):
```html
<span>Message: {{ msg }}</span>
```
The mustache tag will be replaced with the value of the `msg` property on the corresponding data object. It will also be updated whenever the data object’s `msg` property changes.

You can also perform one-time interpolations that do not update on data change by using the v-once directive, but keep in mind this will also affect any other bindings on the same node:
```HTML
<span v-once>This will never change: {{ msg }}</span>
```
#### Raw HTML
The double mustaches interprets the data as plain text,**not HTML**. In order to output real HTML, you will need to use the `v-html` directive:
```HTML
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```
The contents of the `span` will be replaced with the value of the `rawHtml` property, interpreted as plain HTML - data bindings are ignored. Note that you cannot use `v-html` to compose template partials, because Vue is not a string-based templating engine. Instead, components are preferred as the fundamental unit for UI reuse and composition.
#### Attributes
Mustaches cannot be used inside HTML attributes. Instead, use a **v-bind directive**:
```HTML
<div v-bind:id="dynamicId"></div>
```
In the case of boolean attributes, where their mere existence implies `true`, `v-bind` works a little differently. In this example:
```HTML
<button v-bind:disabled="isButtonDisabled">Button</button>
```
If isButtonDisabled has the value of `null`, `undefined`, or `false`, the `disabled` attribute will not even be included in the rendered `<button>` element.