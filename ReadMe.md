# Discriminated unions for JavaScript (ECMAScript)

## What is a discriminated union?

It is a datatype that allows storing values of different shapes, and discriminating between these variants at runtime.

Also called _variant type_, _sum type_.

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

## How would usage look like?

```
switch (x of Fruit) {
  case Apple(clr): 
    alert(`A ${clr} apple a day...`)
    break
  case Orange: 
    alert("A blood orange?")
    break
} else {
  alert("That's not a Fruit")
}
```

`col` would be like a `const`. The above is just a strawman.

## What would be the type?

```
typeof Fruit.Apple == "function"
typeof Fruit.Apple("green") == "tagged string" //??
x instanceof Fruit == true
x instanceof Fruit.Apple == ??
```

