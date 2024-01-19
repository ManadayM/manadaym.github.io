---
title: Angular Signals
description: Notes on Angular Signals.
pubDatetime: 2024-01-17T00:29:00
postSlug: angular-signals
featured: false
draft: false
tags:
  - angular
  - front-end
---

![tp.web.random_picture](https://images.unsplash.com/photo-1517842645767-c639042777db?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXJ8fHx8fHwxNzA1Njc0NDkx&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

Notes on Angular Signals.

## Table of contents

## Introduction

Signals provide a new way for our _code_ to tell our _templates_ (and other code) that our data has changed. It improves Angular's _change detection_ and makes our code more _reactive_.

Observe the following example where `z` will not react to changes in `x` or `y`.

```js
let x = 5;
let y = 3;
let z = x + y;

console.log(z); // => 8

x = 10;

console.log(z); // => 8
```

One of the reasons, we use frameworks/libraries like Angular or React is that **we want a reactive user interface. We want to react to changes**.

For example, when user changes quantity for an item added into the cart, we want the code to react and recalculate the cart total.

Current options to react to such changes are creating `Getters` or `Custom Events`. However, this works in the same component.

```ts
// Getter.
// When the quantity changes the change detection kicks in
// and the template gets the new extended price.
item = "Product XYZ";
price = 19416.13;
quantity = 1;

get exPrice() {
	return price * quantity;
}
```

```ts
// Event
item = "Product XYZ";
price = 19416.13;
quantity = 1;
exPrice = price;

onQuantitySelected(qty: number) {
	exPrice = price * quantity;
}
```

**What if we want the updated price in a different component? That's where signals comes in!**

```ts
// Signals
item = "Product XYZ";
price = 19416.13;

// 'quantity' is marked as a signal.
quantity = signal(1);

// Here, computed signal reacts and recalculates 'exPrice'
// when the 'quantity' signal changes.
exPrie = computed(() => this.price * this.quantity());
```

Here is our rewritten first example using signals.

```ts
const x = signal(5);
const y = signal(3);
const z = computed(() => x() + y());

console.log(z()); // 8

x.set(10);

console.log(z()); // 13
```

## Create a Signal

- We can create a signal using the `signal` constructor function.
- We can also set an optional type where type can be _string_, _number_, _array_, _object_, or any other type.
- **Signal requires a default value.**

```ts
quantity = signal<number>(1);
```

```ts
// Examples

qtyAvailable = signal([1, 2, 3, 4, 5, 6]);

selectedVehicle = signal<Vehicle>({ id: 1, name: "Hector", price: 19234.13 });

vehciles = signal<Vehicle[]>([]);
```

## Read a Signal

We read a signal by calling its getter function. Below are some examples.

```ts
constructor() {
	console.log(this.quantity());
}
```

```html
<option *ngFor="let q of qtyAvailable()">{{ q }}</option>
```

```html
<div>Vehicle: {{ selectedVehicle().name }}</div>
<div>Price: {{ selectedVehicle().price }}</div>
```

## Set / Update a Signal

```ts
// Replace the value.
this.quantity.set(qty);
```

```ts
// Update the value based on the current value.
this.quantity.update(qty => qty * 2);
```

## Computed Signal

- The `computed` function creates a new signal that depends on other signals.
- A computed signal recomputes when its dependent signals change.
- A computed signal is **read only**.
- The computed value is **memoized**, meaning it stores the computed result.

```ts
totalPrice = computed(() => this.price() * this.quantity());
// Here,
// `computed` is a creation function.
// arrow function is a computation function.
```

## Effect for Side Effects

Use an `effect` if you want to run some code when a signal changes.

```ts
effect(() => console.log(this.selectedVehicle()));
```

## References

- [Angular Signals: What? Why? and How? - YouTube Video by Deborah Kurata](https://youtu.be/oqYQG7QMdzw)
