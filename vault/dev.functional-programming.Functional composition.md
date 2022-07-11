---
id: gzly3lvlt6sxs55qpnqtb8y
title: Functional composition
desc: ""
updated: 1657502914410
created: 1657502666107
---

> https://blog.bitsrc.io/functional-programming-composition-2e9b863d8bcb

# **What is** Functional **Composition**

Composition is the process of **composing** small units into bigger units that solve bigger problems. Where Input of one function comes from the output of previous one.

For example, if we want to build a castle 🏰 we’ll have to compose bricks 🧱

# Examples:

Note: as a personal preference **I’ll be using** `pipe` in the examples.

Let’s say we need to build a simple price calculator, where we can apply:

1. Discount
2. Coupon
3. Tax (default = 30%)
4. Service fees (default = 10)
5. Weight-based shipping cost

Let’s first design the API of the price calculator based on the given requirements

```js
const priceCalculator = (
  taxPercentage = 0.3,
  serviceFees = 10,
  price,
  discount,
  percentCoupon,
  valueCoupon,
  weight,
  $PerKg
) => {
  /* logic */
};
```

We defaulted `tax` to 30% and `serviceFees` to 10$. Waiting for the rest of the params

## The bad way (non compositional)

Let’s build it as an atomic mathematical equation:

```js
const priceCalculator = (
  taxPercentage = 0.3,
  serviceFees = 10,
  price,
  discount,
  percentCoupon,
  valueCoupon,
  weight,
  $PerKg
) => {
  return (
    (price -
      price * percentCoupon -
      discount -
      couponValue +
      weight * $PerKg +
      serviceFees) *
    (1 + taxPercentage)
  );
};
```

It does the job. **But** **it has very poor reading, testing, debugging and maintenance experiences.**

## Let’s do it the good way (composition approach)

Let’s compose…

```js
const priceCalculator = (
  taxPercentage = 0.3,
  serviceFees = 10,
  price,
  discount,
  percentCoupon,
  valueCoupon,
  weight,
  $PerKg
) => {
  const applyTax = (val) => val * (1 + taxPercentage);
  const applyServiceFees = (val) => val + serviceFees;
  const applyPercentCoupon = (val) => val - val * percentCoupon;
  const applyValueCoupon = (val) => val - valueCoupon;
  const applyDiscount = (val) => val - discount;
  const applyShippingCost = (val) => val + weight * $PerKg;

  return pipe(
    applyPercentCoupon,
    applyDiscount,
    applyValueCoupon,
    applyShippingCost,
    applyServiceFees,
    applyTax
  )(price);
};
```

This looks so much cleaner, more testable, debuggable and maintainable. All due to the modular mindset we’re adapting to.

We split each operation to be living on its own, then we `pipe` them and apply `price` to the piped functions.

## **Give it a try**

```js
priceCalculator(10); // NaN
```

We got a `NaN` and that’s unexpected, right?! How can we fix this?

## Let’s debug first

Let me introduce a very useful utility to debug chains (`pipe` and `compose`); `inspect` function. It’s very simple. It only logs what it gets, and returns it.

```js
const inspect = (tag) => (x) => {
  console.log(`${tag}: ${x}`);
  return x;
};
```

Now let’s add that to our chain of functions

```js
const priceCalculator = (
  taxPercentage = 0.3,
  serviceFees = 10,
  price,
  discount,
  percentCoupon,
  valueCoupon,
  weight,
  $PerKg
) => {
  const applyTax = (val) => val * (1 + taxPercentage);
  const applyServiceFees = (val) => val + serviceFees;
  const applyPercentCoupon = (val) => val - val * percentCoupon;
  const applyValueCoupon = (val) => val - valueCoupon;
  const applyDiscount = (val) => val - discount;
  const applyShippingCost = (val) => val + weight * $PerKg;

  return pipe(
    inspect("price"),
    applyPercentCoupon,
    inspect("after applyPercentCoupon"),
    applyDiscount,
    inspect("after applyDiscount"),
    applyValueCoupon,
    inspect("after applyValueCoupon"),
    applyShippingCost,
    inspect("after applyShippingCost"),
    applyServiceFees,
    inspect("after applyServiceFees"),
    applyTax
  )(price);
};
```

The results would look something like

```js
priceCalculator(10);
// price: undefined
// after applyPercentCoupon: NaN
//...
```

Oh! The `price` is `undefined`, haha that’s because the `price` is the 3rd parameter, and we’re passing it first instead!
