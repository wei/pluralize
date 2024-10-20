# Pluralize

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
npx jsr add @wei/pluralize
deno add jsr:@wei/pluralize
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

## API Interface

The `pluralize` module offers the following functions:

| Function                                                                       | Description                            |
| ------------------------------------------------------------------------------ | -------------------------------------- |
| `pluralize(word: string, count?: number, inclusive?: boolean): string`         | Main function to pluralize words       |
| `pluralize.plural(word: string): string`                                       | Convert a word to its plural form      |
| `pluralize.singular(word: string): string`                                     | Convert a word to its singular form    |
| `pluralize.addPluralRule(rule: RegExp \| string, replacement: string): void`   | Add a custom pluralization rule        |
| `pluralize.addSingularRule(rule: RegExp \| string, replacement: string): void` | Add a custom singularization rule      |
| `pluralize.addIrregularRule(single: string, plural: string): void`             | Define an irregular pluralization rule |
| `pluralize.addUncountableRule(word: string \| RegExp): void`                   | Specify words without a plural form    |
| `pluralize.isPlural(word: string): boolean`                                    | Check if a word is in plural form      |
| `pluralize.isSingular(word: string): boolean`                                  | Check if a word is in singular form    |

## License

MIT
