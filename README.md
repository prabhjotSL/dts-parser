# dts-parser

TypeScript d.ts parser.

It generates AST like JSON.

See output detail in `lib.d.ts.parsed`.

## Features

- ✔ module
- ✔ nested module
- ✔ class
- ✔ variable declaration
- ✔ string/number/boolean/any/lambda
- ✔ function
- ✔ interface
- ✔ generics in class
- ✔ generics in interface
- ✔ generics in function
- ✔ T[]
- ✔ nullable?
- ✔ class - extends
- ✔ class - implement
- ✔ interface - extends

## Examples

examples/dummy.d.ts

```typescript
declare module Foo {
    export function fun(str?: number[]):void;
    export var a:number;
    export class Bar {
        x: any;
    }
}

export class X {}
export var x: any;

export interface IFoo {
  s: string;
  f: (t:number) => Object[];
}

export interface IFoo2 extends IFOO {
  n : number;
}

```

```
$ npm install -g
$ dts-parser examples/dummy.d.ts
moduleName: Top
modules:
  -
    moduleName: Foo
    modules:
      (empty array)
    classes:
      -
        className:      Bar
        properties:
          -
            propertyName:   x
            typeAnnotation:
              typeName:      Any
              typeArguments:
                (empty array)
              isArray:       false
        typeParameters: null
        heritages:
          implementList: null
          extend:        null
    properties:
      -
        typeAnnotation:
          annotationType: functionType
          returnType:
            typeName:      Void
            typeArguments:
              (empty array)
            isArray:       false
          arguments:
            -
              identifierName: str
              typeAnnotation:
                typeArguments:
                  (empty array)
                isArray:       true
              nullable:       true
        typeParameters: null
      -
        propertyName:   a
        typeAnnotation:
          typeName:      Number
          typeArguments:
            (empty array)
          isArray:       false
    interfaces:
      (empty array)
classes:
  -
    className:      X
    properties:
      (empty array)
    typeParameters: null
    heritages:
      implementList: null
      extend:        null
properties:
  -
    propertyName:   x
    typeAnnotation:
      typeName:      Any
      typeArguments:
        (empty array)
      isArray:       false
interfaces:
  -
    interfaceName:  IFoo
    properties:
      -
        propertyName:   s
        typeAnnotation:
          typeName:      String
          typeArguments:
            (empty array)
          isArray:       false
      -
        propertyName:   f
        typeAnnotation:
          annotationType: lambdaFunctionType
          typeAnnotation:
            typeName:      Object
            typeArguments:
              (empty array)
            isArray:       true
          arguments:
            -
              identifierName: t
              typeAnnotation:
                typeName:      Number
                typeArguments:
                  (empty array)
                isArray:       false
              nullable:       false
    typeParameters: null
    heritages:
      implementList: null
      extend:        null
  -
    interfaceName:  IFoo2
    properties:
      -
        propertyName:   n
        typeAnnotation:
          typeName:      Number
          typeArguments:
            (empty array)
          isArray:       false
    typeParameters: null
    heritages:
      implementList: null
      extend:
        typeName:      IFOO
        typeArguments:
          (empty array)
        isArray:       false
```

## Command Line Interface

```
npm install -g
```

- `-j, --json`: output as json
- `-c`: output with no-color

## Handle as node

```coffee
parser = require 'dts-parser'
console.log parser.parse('declare var x: number;')
```

## Motivations

TypeScript's type definitions are known in its own and has [borisyankov/DefinitelyTyped](https://github.com/borisyankov/DefinitelyTyped "borisyankov/DefinitelyTyped")

## LICENSE

The MIT License (MIT)

Copyright (c) 2014 Koutaro Chikuba

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
