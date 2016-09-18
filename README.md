# Below are v2.0 docs. v1.4.1 docs [here](https://github.com/moroshko/autosuggest-trie/blob/b8c47084049316f45a272ffc678dbd013f073bd4/README.md).

<a href="https://codeship.com/projects/77991" target="_blank">
  <img src="https://img.shields.io/codeship/a3eddcc0-d548-0132-ef15-420032d7f4bd/master.svg?style=flat-square"
       alt="Build Status" />
</a>
<a href="https://codecov.io/gh/moroshko/autosuggest-trie" target="_blank">
  <img src="https://img.shields.io/codecov/c/github/moroshko/autosuggest-trie/master.svg?style=flat-square"
       alt="Coverage Status">
</a>
<a href="https://www.bithound.io/github/moroshko/autosuggest-trie" target="_blank">
  <img src="https://www.bithound.io/github/moroshko/autosuggest-trie/badges/score.svg"
       alt="bitHound Overall Score">
</a>
<a href="https://npmjs.org/package/autosuggest-trie" target="_blank">
  <img src="https://img.shields.io/npm/v/autosuggest-trie.svg?style=flat-square"
       alt="NPM Version" />
</a>

# Autosuggest Trie

Minimalistic trie implementation for autosuggest and autocomplete components.

## Installation

```shell
npm install autosuggest-trie --save
```

## Basic Usage

```js
import createTrie from 'autosuggest-trie';

const locations = [
  {
    id: 1,
    location: 'East Richmond 1234 VIC',
    population: 10000
  },
  {
    id: 2,
    location: 'East Eagle 1235 VIC',
    population: 5000
  },
  {
    id: 3,
    location: 'Richmond West 5678 VIC',
    population: 4000
  },
  {
    id: 4,
    location: 'Cheltenham 3192 Melbourne VIC',
    population: 7000
  },
  {
    id: 5,
    location: 'Richmond 6776 VIC',
    population: 3000
  }
];

const trie = createTrie(locations, 'location');

console.log(trie.getMatches('richmond e'));
/*
  [ { id: 1, location: 'East Richmond 1234 VIC', population: 10000 } ]
*/

console.log(trie.getMatches('ri', { limit: 2 }));
/*
  [ { id: 3, location: 'Richmond West 5678 VIC', population: 4000 },
    { id: 5, location: 'Richmond 6776 VIC', population: 3000 } ]
*/
```

## API

| Function | Description |
| :--- | :--- |
| [`createTrie(items, textKey, options)`](#createTrieFunction) | Creates a trie containing the given items. |
| [`getMatches(query, options)`](#getMatchesFunction) | Returns items that match the given query. |

<a name="createTrieFunction"></a>
### createTrie(items, textKey, options)

Creates a trie containing the given items.

| Parameter | Type | Required | Description |
| :--- | :--- | :---: | :--- |
| `items` | Array | ✓ | Array of items. Every item must be an object. |
| `textKey` | String | ✓ | Key that every `item` in `items` must have.<br />`item` will be inserted to the trie based on `item[textKey]`. |
| `options` | Object | | Additional options |

Possible options:

| Option | Type | Description |
| :--- | :--- | :--- |
| comparator | Function | Items comparator, similar to [`Array#sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)'s `compareFunction`.<br />It gets two items, and should return a number.<br /><br />**Note:** Matches in the first word (let's call it "group 1") are prioritized over matches in the second word ("group 2"), which are prioritized over matches in the third word ("group 3"), and so on.<br />`comparator` will only sort the matches **within each group**.<br /><br />When `comparator` is not specified, items within each group will preserve their order in `items`. |

<a name="getMatchesFunction"></a>
### getMatches(query, options)

Returns items that match the given query.

| Parameter | Type | Required | Description |
| :--- | :--- | :---: | :--- |
| `query` | String | ✓ | Query string |
| `options` | Object | | Additional query options |

Possible options:

| Option | Type | Description |
| :--- | :--- | :--- |
| `limit` | Number | Integer >= 1<br /><br />**For example:** `getMatches('me', { limit: 3 })` will return no more than 3 items that match `'me'`. |

## Running Tests

```shell
npm test
```

## License

<a href="http://moroshko.mit-license.org" target="_blank">MIT</a>
