# reason-react

A Reason introduction for React developers

Fabricio C. Zuardi

CraveFood Systems - August 2018

---

# React

+++

## React introduction 2013

![Video](https://www.youtube.com/embed/XxVg_s8xAms)

Tom Occhino and Jordan Walke spoke about React.js at Facebook Seattle.

Note:

- 2:42 Mutation is complex
- 3:14 One directional data binding
- 5:30 a Javascript Library for building user interfaces 
- 6:00 Declarative components, more than a template…
- 7:31 No explicit data binding
- 8:44 render functions
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
- 2017:
  - Fiber, relicensing of React, Jest and Flow to MIT and…
- 16 Março 2017: [Taming the metalanguage](https://youtu.be/_0T5OSSzxms) - Cheng Lou

@ulend

Note:

- https://en.wikipedia.org/wiki/React_(JavaScript_library)
- first deployed in 2011, Facebook newsfeed and later in Instagram 2012
- influenced by XHP
- react native February 2015 React conf, open sourced in March 2015
- 23 sept 2017 - relicensing
- Introduction to React https://www.youtube.com/watch?v=XxVg_s8xAms

+++

![cheng-lou](https://user-images.githubusercontent.com/7760/43876446-782e8894-9b6b-11e8-81bb-cc5366c16b40.jpg)

+++

---

# Reason

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

---

# Javascript code

___

# Reason code

