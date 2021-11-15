# Select input

The select input uses html's [native select input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select). Select inputs can be single value selections, or multi-value sections by using the `multiple` attribute. There are 4 ways to provide options to a select input:

- As an array of strings
- An object of value/label pairs
- An array of objects with `label` and `value` properties (the same as a [checkbox input](/inputs/checkbox)).
- Using `<option>` tags directly inside the `default` slot.

## Single selection

Select lists are most commonly used to select a single item from a list of options.

### Array of strings

The simplest way to provide options is an array of strings. The provided strings will be used for both the label and the value of the option.

<example
name="Select input - strings"
file="/_content/examples/select-strings/select-strings"
langs="vue"></example>

### Value / Label Object

You may also provide the `options` prop where the keys are values and the values of each property are labels.

<example
name="Select input"
file="/_content/examples/select/select"
langs="vue"></example>

### Array of objects

Them most flexible way to define options is by providing an array of objects. The objects _must_ include `value` and `label` properties — but they may also include a `help` attribute as well as an `attrs` object of additional attributes to apply to each checkbox input tag.

<example
name="Select input - objects"
file="/_content/examples/select-objects/select-objects"
langs="vue"></example>

<callout type="tip" label="Option attributes">
To pass additional attributes to each <code>&lt;option&gt;</code> element your object can also contain an <code>attrs</code> property.<br><br>
<code class="block">[
  {
    label: 'My Label',
    value: 'a-value',
    attrs: {
      disabled: true
    }
  }
]</code>
</callout>

### Default slot

Sometimes it maybe desirable to manually output the contents of a select list in order to create specialized structures. This can be done by using the `default` slot and explicitly outputting your options.

<example
name="Select input - objects"
file="/_content/examples/select-slot/select-slot"
langs="vue"></example>

<callout type="warning">
When using the default slot to output options you should not use the <code>placeholder</code> or <code>options</code> props.
</callout>

## Multiple

The `select` input also supports a `multiple` attribute that allows for multi-selection. When used with FormKit, this option produces an array of values.

<example
name="Select input - objects"
file="/_content/examples/select-multiple/select-multiple"
langs="vue"></example>

<callout type="tip" label="Alternatives">
Select inputs with the <code>multiple</code> attribute can be challenging for some users because they require holding-down the control or command keys to perform multiple selections. Depending on your audience, you may want to consider using a <a href="/inputs/checkbox">checkbox input with <code>options</code></a> instead.
</callout>

<callout type="warning" label="Multiple with default slot">
When using the default slot in conjunction with the <code>multiple</code> attribute you must explicitly assign the <code>selected</code> attribute to each option.
</callout>

## Props & Attributes

<reference-table input="select" :data="[{prop: 'options', type: 'Array/Object', default: '[]', description: 'An object of value/label pairs or an array of strings, or an array of objects that <em>must</em> contain a label and value property.'},{prop: 'placeholder', type: 'String', default: 'none', description: 'When defined FormKit injects a non-selectable hidden <code>option</code> tag as the first value of the list to serve as a placeholder.'}]">
</reference-table>

## Composition keys

<reference-table type="compositionKeys" primary="composition-key" :data="[{'composition-key': 'option', description: 'Responsible for rendering each option. Context includes an <code>option</code> property with the option being rendered. This object includes <code>label</code> and <code>value</code> properties.'}]">
</reference-table>

## Available utilities

[TK] - Masks

[TK] - Casts