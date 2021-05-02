# Discriminated unions for JavaScript (ECMAScript)

## What is a discriminated union?

It is a datatype that allows storing values of different shapes, and discriminating between these variants at runtime.

Also called _variant type_, _sum type_, _tagged_ union.

## How would a declaration look?

```
enum Fruit {
  Apple(color)
  Orange
}

enum More extends Fruit {
  Pear(cultivar, region="China")
}

// Then you can do
const x = Fruit.Apple("red")
```
Or without `Fruit.`?

TypeScript could extend this so you can declare `Apple(color: "red"|"green")`, for example.

Another option is the `Fruit = Apple | Orange | ...` syntax, but I believe the `enum` one is more _JavaScripty_.
[Swift](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html) and [Rust](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html)
have similar syntax.

## How would usage look like?

```
switch (x of Fruit) {
  case Apple(clr): 
    alert(`A ${clr} apple a day...`)
    clr = "foo" // Error: clr is const.
    break
  case Orange: 
    alert("An orange a day?")
    break
} else {
  alert("That's not a Fruit")
}
```

`of Fruit`, so that "Fruit." doesn't need to be repeated in each `case`, also to disambiguate the variants (for example, `ComputerBrand.Apple` could also exist).
And this also gives `else` meaning. Open to other syntax, the above is just a strawman.

Another idea is `case Apple(const color)` or similar, or to forgo `case`.

## What would the type be?

```
typeof Fruit.Apple == "function"
typeof Fruit.Apple("green") == "tagged string" //??
x instanceof Fruit == true
x instanceof Fruit.Apple == also true??
```

I imagine no properties on instances of discriminated unions like `x`.

## See also

Inspired by languages like [ML](https://en.wikibooks.org/wiki/Standard_ML_Programming/Types#Datatype_declarations), and the syntax of [Swift](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html).

