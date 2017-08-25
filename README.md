# n
```clojure

(n expr & forms)

```
like some-> or some->>, except forms following subsequent n's are treated as predicates that do not affect the value passed to the next form.

<img src="http://www.csstoday.com/UploadFiles/Multimedia/2015/4/201504161045388080.jpg"
 alt="Along the river" height="250" />

[![Build Status](https://travis-ci.org/rcullito/n.svg?branch=master)](https://travis-ci.org/rcullito/n)
[![Clojars Project](https://img.shields.io/clojars/v/n.core.svg)](https://clojars.org/n.core)

## About
`n` will thread first or last depending on whether `expr` passed to `n` is `sequential?`

## Usage

Make an assertion about your data. Only proceed if that assertion is truthy.

```clojure

[n.core :refer [n]]

(def person
  {:name "Nancy"
   :dog  "Claire"
   :age 37})

(n person
   (:age)
   (n (> 30))
   inc) => 38

(n person
   (:age)
   (n (> 40))
   inc) => nil

```

If you hit a NullPointerException, you can go back and refactor with n to exit with panache.

```clojure
(->> [1 nil 2]
     (map inc)) => Unhandled java.lang.NullPointerException

(n [1 nil 3]
   (n (every? number?))
   (map inc)) => nil
```

The safeguard won't clutter your business logic when the data holds to the contract.

```clojure
(n [1 2 3]
   (n (every? number?))
   (map inc)) => (2 3 4)

```
