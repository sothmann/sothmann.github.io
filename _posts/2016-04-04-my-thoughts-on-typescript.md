---
title: My Thoughts on TypeScript
layout: post
---

I use [TypeScript](http://www.typescriptlang.org/), the statically typed superset of JavaScript, for almost three years
now on a daily basis in product development.
My team and me are very happy with TypeScript and the development experience. We couldn't imagine going back to plain
JavaScript development.  
From time to time, I'm faced with questions and concerns regarding TypeScript from people who have not used it yet.
I'd like to address some of these questions and concerns in this blog post.
I'm not going to give an introduction to the language and it's features, as there are many sources on the internet that
do this quite well.


### Why is plain JavaScript not enough?

Larger web front ends may be fast to write in JavaScript, but the codebases may become hard to navigate, read and
maintain.
This is primarily due to the lack of static typing and the tooling that static typing renders possible.
Developers who are used to work with statically typed languages and strong tooling on the back end,
e.g. Java or C#, demand features like auto completion, usage search and refactorings.
They also demand common language features like classes, modules and declarative dependencies.

TypeScript addresses these problems and tries to better support the development experience with static typing on the
one hand, and ECMAScript 6+/2015+ language features on the other hand. The static type information is simply discarded
when compiling to JavaScript, while the ECMAScript language features (e.g. classes and modules) are compiled to the
corresponding ES3/5 language constructs so that they become usable in any browser (even ancient browsers like IE6).
The code TypeScript generates is idiomatic (not cryptic) as you can see below.


### How does TypeScript compare to the competition?

Today there are a lot of languages and tools that support either static typing, advanced language features, or both.
Some of the most prominent ones are:

- [GWT](http://www.gwtproject.org/)  
  GWT has been build by Google several years ago. It is mature and powerful. You develop your application using Java as
  the programming language,   so you benefit from the outstanding tooling for Java. GWT treats JavaScript as ByteCode,
  so it generates very cryptic, unreadable code, but the   code is heavily optimized.
  I have used GWT for several years and was very satisfied with the development experience.
  The downside of GWT is that you are relativly far away from the JavaScript ecosystem - you will often use wrappers
  around JavaScript libraries, roll your own wrappers   or you will try to avoid to use libraries of the rich JavaScript
  ecosystem and prefer pure GWT based solutions.
- [Dart](https://www.dartlang.org/)  
  Dart is another approach by Google. It tries to replace JavaScript with a "better" language, that may either be
  compiled to JavaScript, or preferable run inside a VM in the browsers. The latter requires browser vendors to add
  support for Dart to the browsers, and as of today it seems that this will never happen.
  Dart never really started to lift off, and - while being a well crafted language - I personally doubt it ever will.
- [Babel](https://babeljs.io/)  
  Babel is a transpiler that allows to use ECMAScript 6 features today, which gets compiled to corresponding ECMAScript
  constructs that work in older browsers.
  It's quite similar to TypeScript's ES6 to ES3/5 compilation, but Babel does not offer any static typing features.
  So while allowing to use language features like classes and modules that many developers are longing for, for me
  personally this is not enough to improve the development experience. It alone will not make it easier to maintain
  large codebases.
- [Flow](http://flowtype.org/)  
  Facebook's Flow is a superset of JavaScript and focuses on the static typing features only.
  The Flow team works together with the TypeScript team and they ensure that both projects share the same syntax for
  type annotations. In contrast to TypeScript today, Flow also provides runtime type checks
  (TypeScript offers compile time type checks only).

While GWT and Dart try to replace JavaScript with completely different languages, TypeScript embraces JavaScript and
adds the missing pieces.
The combination of Babel and Flow comes really close to what TypeScript offers, and the syntax should be
almost identical.
Babel and Flow are more popular in the React camp, while TypeScript is more popular in the Angular camp
(in fact Angular 2.0 is built with TypeScript, and TypeScript seems to be the recommended language for
Angular 2.0 based app development).

TypeScript is very well supported by various IDEs.
Java developers - like me - will enjoy to use TypeScript with either Eclipse or IntelliJ IDEA.

Flow lacks support by major IDEs.
Facebook offers their own Atom based IDE ([Nuclide](http://nuclide.io/)).
I'm not sure how well this IDE supports Babel.
At least developers would have to use two different IDEs for front end and back end development,
and two tools (instead of one) have to be integrated into the build tool chain.


### How proprietary is TypeScript? How mature or experimental are the ECMAScript features offered by TypeScript?

TypeScript's static typing features are proprietary, there is no standard for it.
But at least Google, Facebook and Microsoft reached consensus that this is the syntax for static typing in JavaScript.
Maybe one day we will see static typing in the ECMAScript standard, but that is pure speculation.
As the web standards are driven by companies like Google, Facebook and Microsoft, there is at least a chance.
And if static typing will be baked into the future standard, it will likely have the syntax of TypeScript.

The other language features are primarily ES6/ES2015 features. This standard has been finalized in 2015, so it is
stable, reliable stuff. There are some features of ES7/2016+ supported, but these features have to be enabled by a
compiler flag and are explicitly stated as being experimental, so it's easy to avoid them.
If you want to play it safe, use only the ES6 features.


### It's from Microsoft

People seem to think Microsoft is evil, and that you should avoid using their technologies.

While I think that this is a pointless argument, I can at least understand these concerns.
But Microsoft has changed a lot in the last years - especially since Satya Nadella became the CEO and has dramatically
rebalanced the company's strategies. Microsoft has released e.g. dotNet, the C# compiler and IE's JavaScript engine as
open source projects on GitHub, and more and more projects follow.
[TypeScript is one of these open source projects found on GitHub](https://github.com/microsoft/typescript),
using the liberal Apache 2 license.
Microsoft accepts pull requests and manages the issues on GitHub.
For me, this is as open as open source could be.
Microsoft even joined the Eclipse foundation and embraces Linux (e.g. they announced SQL Server for Linux
and the Linux subsystem for Windows 10).

This is not the Microsoft that people know from the past.
Old prejudices should be reconsidered.


### What if Microsoft abandons TypeScript? What would we lose?

TypeScript is open source, Apache 2 licensed, so even without Microsoft support, I think the project would be viable,
as the community has grown to a point where I think others would jump in and continue development.
But I doubt that could happen any time soon.
Microsoft uses TypeScript heavily internally, e.g. in Visual Studio Online, Visual Studio Code, Team Foundation Server,
BING picture search and Xbox Music.

But even if TypeScript is abandoned or you decide that you don't want to continue with TypeScript, there is an
exit strategy. As the generated code is idiomatic, you could just continue with the generated JavaScript code.
The static type annotations would be lost, but without TypeScript, you would not have these type annotations anyway.

Alternatively, you could switch to the combination of Babel and Flow.
I would expect that it only requires little changes to the code.


### What are the downsides of TypeScript?

Everything in life has its price.
Compared to plain JavaScript development, TypeScript (as well as it's competitors) requires the usage of a compiler.
The compiler needs to be integrated into your tool chain.
As integrations for many IDEs exist, as well as integrations into popular build tools like Grunt, Gulp, Maven and
Gradle, the integration is easy and straightforward.

Regarding debugging, TypeScript supports source maps, so you can debug the original TypeScript source code in the
browser. However a browser with support for source maps is required.
All major browsers like Chrome, Firefox and Internet Explorer support source maps, but IE support starts with
version 11 only.
But even if you are in the bad position that your browser doesn't support source maps, the idiomatic code generated by
TypeScript is easy to debug in compiled form.
I know it's not the same, but it is absolutely doable.


### How idiomatic is the generated code?

From my point of view, the generated code is very idiomatic.
It's probably better code than what a lot of developers would write on their own.
As Douglas Crockford once said:
"Microsoft's TypeScript may be the best of the many JavaScript front ends. It seems to generate the most attractive code.".
I totally agree.
TypeScript's ECMAScript stuff gets transformed to corresponding ES3 or ES5 variants using established
JavaScript design patterns and best practices. TypeScript's static typing features like type annotations and interfaces
are pure compile time constructs, so the compiler simply eliminates them in the JS output.
Here are some examples.

The following snippet shows the usage of type annotations and how they are eliminated in the JavaScript output:

```javascript
// TS
function multiply(a: number, b: number): number {
  return a * b;
}
```

```javascript
// JS
function multiply(a, b) {
  return a * b;
}
```

In this example, you see that interfaces are pure compile time constructs that are eliminated when being compiled
to JavaScript:

```javascript
// TS
interface Point {
  x: number;
  y: number;
}

function drawLine(from: Point, to: Point) {
  console.log("Drawing line...");
}
```

```javascript
// JS
function drawLine(from, to) {
  console.log("Drawing line...");
}
```

Here you can see the usage of namespaces.
Namespaces are compiled to the revealing module pattern.
A potentially already existing namespace object is past to an [immediately-invoked function expression](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression),
and it gets extended with the exported function.

```javascript
// TS
namespace greetings {
  var greetingText = "hello world!"; 
  export function greet() {
    console.log(greetingText);
  }
}
```

```javascript
// JS
var greetings;
(function (greetings) {
  var greetingText = "hello world!";
  function greet() {
    console.log(greetingText);
  }
  greetings.greet = greet;
})(greetings || (greetings = {}));
```

Here you see how classes are compiled to ES 3 or 5.
Again, an [immediately-invoked function expression](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression)
is used for scoping, a constructor function is defined and the prototype chain is established.

```javascript
// TS
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}

var greeter = new Greeter("world");
```

```javascript
// JS
var Greeter = (function () {
  function Greeter(message) {
    this.greeting = message;
  }
  Greeter.prototype.greet = function () {
    return "Hello, " + this.greeting;
  };
  return Greeter;
}());
var greeter = new Greeter("world");
```


### What about WebAssembly?

WebAssembly could be the next big thing. I am looking forward to it and I would embrace it.
It is the ByteCode for the Web, and all the major Browser vendors (Mozilla, Google, Microsoft and Apple)
reached consensus. So this actually has a chance to be successful.
But this is a technology of the future - it will take years until WebAssembly will be usable in all major browsers,
and a completely new ecosystem has to be created.
Until then, TypeScript is a good solution for me.


### Conclusion

I hope that I addressed most concerns people have with TypeScript in this post.
There are alternatives, and they seems to be pretty good.
But for me, at the moment there is no better choice that offers the same set of language features,
hassle-free JavaScript integration and tooling.
If you are looking for a JavaScript remedy, you should at least consider TypeScript.
