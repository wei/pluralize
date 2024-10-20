[![pluralize](https://socialify.git.ci/wei/pluralize/image?description=1&language=1&name=1&owner=1&pattern=Diagonal%20Stripes&theme=Auto)](https://socialify.git.ci/wei/pluralize?description=1&language=1&name=1&owner=1&pattern=Diagonal%20Stripes&theme=Auto)

> A Deno module to pluralize and singularize English words.

Pluralize and singularize any word with ease!

This is a TypeScript fork of the original
[pluralize](https://github.com/plurals/pluralize) project, providing full
TypeScript support and Deno compatibility.

## Why Pluralize?

This module employs a pre-defined list of rules, applied in order, to
singularize or pluralize given words. It's particularly useful for:

- Automating processes based on user input
- Handling dynamic content where word forms may vary

For applications where words are known ahead of time, a simple ternary operation
or custom function would be a lighter alternative.

## Installation

Pluralize is available on [jsr](https://jsr.io/@wei/pluralize). You can install
it using the following command:

```bash
deno add jsr:@wei/pluralize
npx jsr add @wei/pluralize
```

## Usage

```typescript
import { pluralize } from "pluralize";
```

### Basic Pluralization

Convert a word to its plural form:

```typescript
console.log(pluralize("test")); //=> "tests"
```

### Count-Based Pluralization

Specify a count to get the correct form:

```typescript
console.log(pluralize("test", 0)); //=> "tests"
console.log(pluralize("test", 1)); //=> "test"
console.log(pluralize("test", 5)); //=> "tests"
```

### Inclusive Count

Include the count in the output:

```typescript
console.log(pluralize("test", 1, true)); //=> "1 test"
console.log(pluralize("test", 5, true)); //=> "5 tests"
```

### Handling Non-English Words

The module also supports non-English words:

```typescript
console.log(pluralize("蘋果", 2, true)); //=> "2 蘋果"
```

### Custom Rules

#### Adding Custom Plural Rules

```typescript
pluralize.addPluralRule(/gex$/i, "gexii");
console.log(pluralize.plural("regex")); //=> "regexii"
```

#### Adding Custom Singular Rules

```typescript
pluralize.addSingularRule(/singles$/i, "singular");
console.log(pluralize.singular("singles")); //=> "singular"
```

#### Irregular Rules

Define irregular pluralization rules:

```typescript
pluralize.addIrregularRule("irregular", "regular");
console.log(pluralize.plural("irregular")); //=> "regular"
```

#### Uncountable Rules

Specify words that do not have a plural form:

```typescript
pluralize.addUncountableRule("paper");
console.log(pluralize.plural("paper")); //=> "paper"
```

### Checking Word Forms

Determine if a word is singular or plural:

```typescript
console.log(pluralize.isPlural("test")); //=> false
console.log(pluralize.isSingular("test")); //=> true
```

## API

The `pluralize` module provides the following functions:

### `pluralize(word: string, count?: number, inclusive?: boolean): string`

- Converts a word to its plural form based on the count.
- If `inclusive` is true, it includes the count in the output.

### `addPluralRule(rule: RegExp, replacement: string): void`

- Adds a custom pluralization rule.

### `addSingularRule(rule: RegExp, replacement: string): void`

- Adds a custom singularization rule.

### `addIrregularRule(singular: string, plural: string): void`

- Defines an irregular pluralization rule.

### `addUncountableRule(word: string): void`

- Specifies a word that does not have a plural form.

### `isPlural(word: string): boolean`

- Checks if the given word is plural.

### `isSingular(word: string): boolean`

- Checks if the given word is singular.

## License

MIT
