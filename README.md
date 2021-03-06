# dts-parser

[![Build Status](https://drone.io/github.com/mizchi/dts-parser/status.png)](https://drone.io/github.com/mizchi/dts-parser/latest)

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

## Install

```
npm install dts-parser -g
```

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
nodeType:   TopModule
moduleName: Top
modules: 
  - 
    nodeType:   Module
    moduleName: Foo
    modules: 
      (empty array)
    classes: 
      - 
        nodeType:       ClassNode
        className:      Bar
        properties: 
          - 
            nodeType:       VariableNode
            propertyName:   x
            typeAnnotation: 
              nodeType:      AnnotatedType
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
        propertyName:   fun
        typeAnnotation: 
          nodeType:   Function
          returnType: 
            nodeType:      AnnotatedType
            typeName:      Void
            typeArguments: 
              (empty array)
            isArray:       false
          arguments: 
            - 
              nodeType:       FunctionArgument
              identifierName: str
              typeAnnotation: 
                nodeType:      AnnotatedType
                typeArguments: 
                  (empty array)
                isArray:       true
              nullable:       true
              spriced:        false
        typeParameters: null
      - 
        nodeType:       VariableDeclarationNode
        propertyName:   a
        typeAnnotation: 
          nodeType:      AnnotatedType
          typeName:      Number
          typeArguments: 
            (empty array)
          isArray:       false
    interfaces: 
      (empty array)
classes: 
  - 
    nodeType:       ClassNode
    className:      X
    properties: 
      (empty array)
    typeParameters: null
    heritages: 
      implementList: null
      extend:        null
properties: 
  - 
    nodeType:       VariableDeclarationNode
    propertyName:   x
    typeAnnotation: 
      nodeType:      AnnotatedType
      typeName:      Any
      typeArguments: 
        (empty array)
      isArray:       false
interfaces: 
  - 
    nodeType:       InterfaceNode
    interfaceName:  IFoo
    properties: 
      - 
        nodeType:       VariableDeclarationNode
        propertyName:   s
        typeAnnotation: 
          nodeType:      AnnotatedType
          typeName:      String
          typeArguments: 
            (empty array)
          isArray:       false
      - 
        nodeType:       VariableDeclarationNode
        propertyName:   f
        typeAnnotation: 
          nodeType:       LambdaFunctionAnnotation
          annotationType: lambdaFunctionType
          typeAnnotation: 
            nodeType:      AnnotatedType
            typeName:      Object
            typeArguments: 
              (empty array)
            isArray:       true
          arguments: 
            - 
              nodeType:       FunctionArgument
              identifierName: t
              typeAnnotation: 
                nodeType:      AnnotatedType
                typeName:      Number
                typeArguments: 
                  (empty array)
                isArray:       false
              nullable:       false
              spriced:        false
    typeParameters: null
    heritages: 
      implementList: null
      extend:        null
  - 
    nodeType:       InterfaceNode
    interfaceName:  IFoo2
    properties: 
      - 
        nodeType:       VariableDeclarationNode
        propertyName:   n
        typeAnnotation: 
          nodeType:      AnnotatedType
          typeName:      Number
          typeArguments: 
            (empty array)
          isArray:       false
    typeParameters: null
    heritages: 
      implementList: null
      extend: 
        nodeType:      AnnotatedType
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

## Use as node module

```
$ npm install dts-parser
```

```coffee
parser = require 'dts-parser'
console.log parser.parse('declare var x: number;')
```

## Test

```
$ npm install
$ ./update-fixtures
$ npm test
```

`test/parsed` have generated json by `./update-fixtures` from `test/fixtures`.

Tests compare pre-generated json to json generated by current parser.

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
