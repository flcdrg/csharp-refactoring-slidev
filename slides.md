---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Refactoring C#
info: |
  Refactoring examples based on Martin Fowler's 'Refactoring. Improving the design of existing code', 2nd edition, 2019, Pearson Education

# apply unocss classes to the current slide
# class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Refactoring C# examples

Presentation slides for developers

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/flcdrg/csharp-refactoring-slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# Extract Function

````md magic-move {lines: true}

```csharp {*|6-8}
// before
public void PrintOwing()
{
    var outstanding = calculateOutstanding();

    // print details
    Console.WriteLine("name:"  + _name);
    Console.WriteLine("amount:" + outstanding);
}
```

```csharp {6,9-13|*}
// after
public void PrintOwing()
{
    var outstanding = calculateOutstanding();

    printDetails(outstanding);
}

private printDetails(string name, decimal outstanding)
{
    Console.WriteLine("name: {0}", name);
    Console.WriteLine("amount: {0}", outstanding);
}
```

````

---

# Inline Function

````md magic-move {lines: true}

```csharp {*|4,7-10}
// before
public int GetRating(Driver driver)
{
    return MoreThanFiveLateDeliveries(driver) ? 2 : 1;
}

public bool MoreThanFiveLateDeliveries(Driver driver)
{
    return driver.numberOfLateDeliveries > 5;
}

```

```csharp {*}
// after
public int GetRating(Driver driver)
{
    return (driver.numberOfLateDeliveries > 5) ? 2 : 1;
}
```

````

---

# Extract Variable

````md magic-move {lines: true}

```csharp {*|2|3|4}
// before
return order.Quantity * order.ItemPrice 
  - Math.Max(0, order.Quantity - 500) * order.ItemPrice * 0.05 
  + Math.Min(order.Quantity * order.ItemPrice * 0.1, 100);

```

```csharp {2|3|4|*}
// after
var basePrice = order.Quantity * order.ItemPrice;
var quantityDiscount = Math.Max(0, order.Quantity - 500) * order.ItemPrice * 0.05;
var shipping = Math.Min(order.Quantity * order.ItemPrice * 0.1, 100);
return basePrice - quantityDiscount + shipping;
```

````

---

# Inline Variable

````md magic-move {lines: true}

```csharp {*|2}
// before
var basePrice = order.BasePrice;
return (basePrice > 1000);
```

```csharp {*}
// after
return order.BasePrice > 1000;
```

````

---

# Change Function Declaration

## Rename Function

````md magic-move {lines: true}

```csharp {*|4}
// before
public Circum(double radius)
{
  return 2 * Math.PI * radius;
}
```

```csharp {4|7-10|*}
// extract function
public Circum(double radius)
{
  return Circumference(radius);
}

public Circumference(double radius)
{
  return 2 * Math.PI * radius;
}
```

```csharp {*}
// inline function
public Circumference(double radius)
{
  return 2 * Math.PI * radius;
}
```

````
