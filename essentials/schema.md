# Schema

FormKit's schema is a JSON-serializable data format for storing DOM structures and component implementations including FormKit forms. Although created specifically for implementing forms the format is capable of generating any HTML markup or using any third party components. Schemas are rendered using FormKit's `<FormKitSchema>` component.

A schema is an array of objects, where each object defines a single HTML element or component. These two object types have their own structural definition.

## HTML Elements ($el)

HTML elements are defined using `$el` property. You can use `$el` to render any HTML element. Attributes can be added with the `attrs` property, and content is
assigned with the `children` property.

<example
  name="Schema - elements"
  file="/_content/examples/schema-elements/schema-elements"
  langs="vue"
  layout="row">
</example>

<callout type="tip" name="The style attribute">
Notice in the above example that the <code>style</code> attribute is unique in that it should be defined as an object of style to value pairs rather than a string.
</callout>

## Components ($cmp)

Components can be defined with the `$cmp` property. The `$cmp` property should be a string that references a globally defined component or a component passed
into `FormKitSchema` with the `library` prop.

<example
  name="Schema - components"
  file="/_content/examples/schema-components/schema-components"
  langs="vue"
  layout="row">
</example>

<callout type="warning" label="Components as props">
In order to pass concrete components via the <code>library</code> prop it's best to wrap your library with <a href="https://v3.vuejs.org/api/basic-reactivity.html#markraw">Vue’s <code>markRaw</code> signature</a>.
</callout>

## References

In addition to the schema array (and optional library) the `FormKitSchema` object can also include a `data` prop. Values from the data object can then be referenced directly in your schema — and your schema will maintain the reactivity of the original data object.

To reference a value from the data object, you simply use a dollar sign `$` followed by the property name from the data object. References can be used in `attrs`, `props`, conditionals and as `children`.

<example
  name="Schema - data"
  file="/_content/examples/schema-data/schema-data"
  langs="vue"
  layout="row">
</example>

<callout type="warning" label="Important note">
Notice in the above example that we used an array to concatenate "Hello" and "$location". We did this because data references and logical expressions in the schema must always begin with a dollar sign <code>$</code> — otherwise they are treated as unparsed string literals.
</callout>

### Referencing functions

Schemas support calling functions that are in your original reference data — and you can even pass data references as arguments of that function!

<example
  name="Schema - functions"
  file="/_content/examples/schema-functions/schema-functions"
  langs="vue"
  layout="row">
</example>

### Deep references

Just like JavaScript — you can access properties of a deeply nested object using dot-syntax `object.property`.

<example
  name="Schema - functions"
  file="/_content/examples/schema-dot-syntax/schema-dot-syntax"
  langs="vue"
  layout="row">
</example>

## Expressions

Schemas also support expressions like and boolean logic, comparisons and arithmetic. These expressions can be used anywhere a data reference can be used (`attrs`, `props`, conditionals, and `children`).

<example
  name="Schema - expressions"
  file="/_content/examples/schema-expressions/schema-expressions"
  langs="vue"
  layout="row">
</example>

<callout type="tip" label="Labeling expressions">
Expressions must always begin with a <code>$</code> — if the first element of an expression is a data reference (ex: <code>$count + 2</code>), then it already will begin with a <code>$</code> and no further labeling is required. However often the first character of an expressions is not a dollar sign — these expressions need to be "labeled" with <code>$:</code> — for example <code>$: ($count * 3) - 7</code>
</callout>

Although it looks very much like JavaScript — *schema expressions are not JavaScript*. They are better thought of as a templating language. Expressions are compiled down to functional JavaScript at `setup` but the syntax is not 1-1 compatible with JavaScript. This improves performance, and provides a critical layer of security as only explicitly exposed data an functionality can be executed.

Schema expressions are limited to the following operators and parenthesis:

| Operator | Use case              |
| -------- | --------------------- |
| `+`      | Addition              |
| `-`      | Subtraction           |
| `*`      | Multiplication        |
| `/`      | Division              |
| `%`      | Modulus               |
| `&&`     | Boolean AND           |
| `\|\|`   | Boolean OR            |
| `===`    | Strict equals         |
| `!==`    | Strict not equals     |
| `==`     | Loose equals          |
| `!=`     | Loose not equals      |
| `>=`     | Greater than or equal |
| `<=`     | Less than or equal    |
| `>`      | Greater than          |
| `<`      | Less than             |

## Conditionals

FormKit schema can leverage references and expressions to make schema nodes and attributes conditional. These conditionals can be added in two ways:

- The `if` property on `$el` and `$cmp` nodes.
- The `if/then/else` logic node

### The `if` property

Both `$el` and `$cmp` schema nodes can leverage an `if` property that roughly equates to a `v-if` in Vue. If the expression assigned to the `if` property is truthy, the node is rendered, otherwise it is not.

<example
  name="Schema - conditional"
  file="/_content/examples/schema-conditional/schema-conditional"
  langs="vue"
  layout="row">
</example>

### The `if/then/else` object

The `if/then/else` object can be used anywhere you would normally use a schema node to conditionally render one or many nodes at a time, and optionally an `else` statement. You can also nest `if/then/else` objects to create logic equivalent to `else if`.

<example
  name="Schema - conditional object"
  file="/_content/examples/schema-conditional-object/schema-conditional-object"
  langs="vue"
  layout="row">
</example>

Conditional statements can be used to render attributes.

<example
  name="Schema - conditional attrs"
  file="/_content/examples/schema-conditional-attrs/schema-conditional-attrs"
  langs="vue"
  layout="row">
</example>