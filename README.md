# decimal-to-binary-converter

[![NPM version][npm-svg]][npm]
[![Build status][travis-svg]][travis]
[![Code coverage][codecov-svg]][codecov]

[travis]: https://travis-ci.org/zugarzeeker/decimal-to-binary-converter
[travis-svg]: https://img.shields.io/travis/zugarzeeker/decimal-to-binary-converter.svg?style=flat
[npm]: https://www.npmjs.com/package/decimal-to-binary-converter
[npm-svg]: https://img.shields.io/npm/v/decimal-to-binary-converter.svg?style=flat
[codecov]: https://codecov.io/gh/zugarzeeker/decimal-to-binary-converter/src/master/README.md
[codecov-svg]: https://img.shields.io/codecov/c/github/zugarzeeker/decimal-to-binary-converter.svg

This library is an algorithm for converting decimal to binary and show each steps of calculation.

This library was generated by `essay`(https://github.com/dtinth/essay).

## Getting started
  1. Install this library

  ```
  npm i --save decimal-to-binary-converter
  ```

  2. import function from this library
  ```js
  import { converter } from 'converter'
  ```


## API
`converter` is a function that can be used.

*Limitation: floating point of binary maximum default is 10*

```js
// main.js
export { converter } from './converter'
```

## Example
There are some examples about simple results of `converter`.

```js
// converter.test.js
import { expect } from 'chai'
import { converter, convertFloatToBinary, convertIntegerToBinary } from './converter'

describe('Converter', () => {
  it('should convert decimal 8 to binary 1000', () => {
    expect(convertIntegerToBinary(8)).to.equal('1000')
  })

  it('should convert decimal 0.125 to binary 0.001', () => {
    expect(convertFloatToBinary(0.125)).to.equal('0.001')
  })

  it('should convert decimal 12.875 to binary 1100.111', () => {
    expect(converter(12.875)).to.equal('1100.111')
  })
})
```

## Implementation
`converter` contains two parts
- `convertIntegerToBinary`
- `convertFloatToBinary`

```js
// converter.js
import _ from 'lodash'

export const convertIntegerToBinary = (number) => {
  const result = []
  console.log(`\nConverting Integer ${number} to binary`)
  while (number !== 0) {
    console.log(`\n${number} % 2 = ${number % 2}`)
    console.log(`${number} / 2 = ${number / 2 | 0}`)
    result.push(number % 2)
    number = number / 2 | 0
  }
  const answer = _.reverse(result).join('')
  console.log(`\n[Answer = ${answer}]`)
  return answer
}

export const convertFloatToBinary = (number) => {
  const result = []
  console.log(`\nConverting Float ${number} to binary`)
  while (!_.has(result, number) && number % 1 !== parseFloat(0)) {
    console.log(`\n${number} * 2 = ${number * 2}`)
    console.log(`${number | 0}`)
    number *= 2
    result.push(number | 0 === 1 ? 1 : 0)
    number %= 1
    if (result.length > 10) break
  }
  const answer = `0.${result.join('')}`
  console.log(`\n[Answer = ${answer}]`)
  return answer
}

export const converter = (number) => {
  const intPart = number | 0
  const floatPart = number % 1
  const resultIntPart = convertIntegerToBinary(intPart)
  const resultFloatPart = convertFloatToBinary(floatPart).split('.').pop()
  const result = `${resultIntPart}.${resultFloatPart}`
  console.log(`======== binary of ${number} is ${result} ========`)
  return result
}

```
