# reason-react

A Reason introduction for React developers

Fabricio C. Zuardi

CraveFood Systems - August 2018

+++

Bom dia!

---

# React

+++

## What & Why

![Video](https://www.youtube.com/embed/XxVg_s8xAms)

Tom Occhino and Jordan Walke spoke about React.js at Facebook Seattle.

Note:

- 5:30 a Javascript Library for building user interfaces 
- 6:00 Declarative components, more than a template…
- 8:44 render functions
- 3:14 One directional data binding
- 2:42 Mutation is complex
- 7:31 No explicit data binding
- 12:18 Jordan Walke
- 14:30 JSX
- 24:14 Instagram.com
- 25:30 Open Source

+++

## Timeline

@ul

- created by Jordan Walke @ Facebook
- motivation: FB Chat rewrite, avoid mutations on 
- 2013: open sourced ([video](https://youtu.be/XxVg_s8xAms))
- 2014: Flux better promoted ([video](https://youtu.be/nYkdrAPrdcw?t=10m22s))
- 2015: Redux ([video](https://www.youtube.com/watch?v=xsSnOQynTHs))
- 2015: React Native
- 2017: Fiber, relicensing of React, Jest and Flow to MIT and…
- 16 Março 2017: [Taming the metalanguage](https://youtu.be/_0T5OSSzxms) - Cheng Lou

@ulend

Note:

- https://en.wikipedia.org/wiki/React_(JavaScript_library)
- first deployed in 2011, Facebook newsfeed and later in Instagram 2012
- influenced by XHP
- react native February 2015 React conf, open sourced in March 2015
- 23 sept 2017 - relicensing
- Introduction to React https://www.youtube.com/watch?v=XxVg_s8xAms

---

# Reason

+++

## What & Why

> Reason is not a new language; it's a new syntax and toolchain powered by the battle-tested language, OCaml. Reason gives OCaml a familiar syntax geared toward JavaScript programmers, and caters to the existing NPM/Yarn workflow folks already know.

+++

## Jordan Walke again

- Entrevista (Jun 2018) https://reason.town/jordan-interview

![image](https://user-images.githubusercontent.com/7760/43872979-eb2c7056-9b5a-11e8-8c31-26bf8d6e4c9f.png)


Note:
- fan o StandardML language
- some of the original prototypes of React were written in standardML
- problems implementing the react component model
- I didnt have a lot of primitives in standardML that OCaml have
- I didnt know OCaml at the time
- at the time Js was the way of running anything on the web
- and even if it was not, it was a **hard sell**
- 00:40 - 057 **first react prototypes**
- 01:53 - 2:13 **hard sell**
- 02:39 - 03:40 **reset the precedence**
- 14:28 - Ocaml in production / battle-tested
- 20:13 - incremental adoption / new language


start of 2016, studying concurrency to solve react problems

while studying hard concurrency problems of react, he remembered
how StandardML help him model the problems back when prototyping react

so JW starts to describe those hard problems in Ocaml to help him think. As a tool.

Pattern Matching was super helpful. (concurrent UI problem)

OCaml looks like an alien language

work on developing an Ocaml grammar and a toolchain
partnership with Bob (buckescript)

avoid mutation by default

fully static type language
with abstract data types and pattern matching

if it compiles, you can be confident about not having a full set of possible runtime errors


Hack, Flow, Infer

Objective C -> Swift
Java -> Kotlin
ES5 -> Jquery / Cofeescript -> Babel / ES6 -> Flow / Typescript -> Elm / Closurescript / Reason 

+++

## Taming the meta language

![video](https://www.youtube.com/embed/_0T5OSSzxms)

+++

## Taming the meta language

![cheng-lou](https://user-images.githubusercontent.com/7760/43876446-782e8894-9b6b-11e8-81bb-cc5366c16b40.jpg)

---

# Javascript code

+++

## Setup

```shell
yarn add react react-dom
yarn add --dev babel-preset-env\
               babel-preset-react\
               babel-preset-stage-2
```

+++

## JSX

```jsx
import React from "react";
import ReactDOM from "react-dom";

const msg = "Hello React";
const targetElement = document.getElementById("demo");

const hello = <h1>{msg}</h1>;

ReactDOM.render(hello, targetElement);
```
@[7](tags inside javascript)

+++

### Stateless component

```jsx
import React from "react";
import PropTypes from "prop-types";
import ReactDOM from "react-dom";

const msg = "Hello React";
const targetElement = document.getElementById("demo");

const ColorHello = ({ color, children }) => (
  <h1 style={{ color }}>{children}</h1>
);
ColorHello.propTypes = {
  color: PropTypes.string,
  children: PropTypes.node
};

ReactDOM.render(<ColorHello color="blue">{msg}</ColorHello>, targetElement);
```
@[8-10](component is a function)

+++

## Stateful Component

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  render = () => <div>{this.state.count}</div>;

  componentDidMount = () => {
    this.intervalId = window.setInterval(
      () => this.setState({ count: this.state.count + 1 }),
      1000
    );
  };

  componentWillUnmount = () => window.clearInterval(this.intervalId);
}

ReactDOM.render(<Counter />, targetElement);
```

+++

## Stateful Component

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  render = () => <div>{this.state.count}</div>;

  componentDidMount = () => {
    this.intervalId = window.setInterval(
      () => this.setState({ count: this.state.count + 1 }),
      1000
    );
  };

  componentWillUnmount = () => window.clearInterval(this.intervalId);
}

ReactDOM.render(<Counter />, targetElement);
```

@[2](initial state)
@[4](render function)
@[6,11,13](lifecycle methods)
@[8](setstate)
---

# Reason code

+++

## Setup

```bash
yarn global add bs-platform
bsb -init my-react-app -theme react
```

+++

## JSX

```ocaml
let msgElement = "Hello Reason" |> ReasonReact.string;

let hello = <h1> msgElement </h1>;

ReactDOMRe.renderToElementWithId(hello, "redemo");
```
@[1](reason JSX is more strict about text nodes)
@[1](reverse-application operator, aka pipe)

+++

## Stateless Component

```ocaml
module ColorHello = {
  let component = ReasonReact.statelessComponent("ColorHello");
  let style = ReactDOMRe.Style.make;
  let make = (~color, children) => {
    ...component, 
      render: _self => <h1 style={style(~color=color, ())}> ...children </h1>
  };
}

ReactDOMRe.renderToElementWithId(<ColorHello color="blue"> msgElement </ColorHello>, "redemo");
```

@[1,8](files are modules, and modules are first class citizens)
@[4,7](ReasonReact doesn't use/need classes. The component creation API gives you a plain record, whose fields (like render) you can override.)
@[4](~color is a named argument)
@[2,5](this method will create a record template for stateless component, the string is the displayName)
@[6](use underscore on the start of a variable name to prevent unused var warnings)
@[6](...children is used because children is always an array of elements)

+++

## Reducer Component

```
module Counter = {
  type state = {count: int};
  type action =
    | Increase;
  let component = ReasonReact.reducerComponent("Counter");

  let make = _children => {
    ...component,
    initialState: () => {count: 0},
    render: self => {
      let countNode = self.state.count |> string_of_int |> ReasonReact.string;
      <div> countNode </div>;
    },
    reducer: (action, state) =>
      switch (action) {
      | Increase => ReasonReact.Update({count: state.count + 1})
      },
    didMount: self => {
      let intervalId =
        Js.Global.setInterval(() => self.send(Increase), 1000);
      self.onUnmount(() => Js.Global.clearInterval(intervalId));
    },
  };
};

ReactDOMRe.renderToElementWithId(<Counter />, "redemo");
```

+++

## Reducer Component

```
module Counter = {
  type state = {count: int};
  type action =
    | Increase;
  let component = ReasonReact.reducerComponent("Counter");

  let make = _children => {
    ...component,
    initialState: () => {count: 0},
    render: self => {
      let countNode = self.state.count |> string_of_int |> ReasonReact.string;
      <div> countNode </div>;
    },
    reducer: (action, state) =>
      switch (action) {
      | Increase => ReasonReact.Update({count: state.count + 1})
      },
    didMount: self => {
      let intervalId =
        Js.Global.setInterval(() => self.send(Increase), 1000);
      self.onUnmount(() => Js.Global.clearInterval(intervalId));
    },
  };
};

ReactDOMRe.renderToElementWithId(<Counter />, "redemo");
```

@[5](ReasonReact stateful components are like ReactJS stateful components, except with the concept of "reducer" (like Redux) built in)
@[2](state can be of any type)
@[3-4](a variant of all the possible state transitions in your component. In state machine terminology, this'd be a "token")
@[9](initial state)
@[14-16](state transitions)
@[18,22](lifecycle events)
@[21]( ReasonReact provides a helper field in self, called onUnmount (see [Subscription helpers](https://reasonml.github.io/reason-react/docs/en/subscriptions-helper)))
@[21](BuckleScript is mostly a compiler, but it does ship some libraries for users' convenience )

