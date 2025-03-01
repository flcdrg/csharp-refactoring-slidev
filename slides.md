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
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# Extract function


````md magic-move {lines: true}

```csharp {*|6-8}
// step 1
public void PrintOwing()
{
    var outstanding = calculateOutstanding();

    // print details
    Console.WriteLine("name:"  + _name);
    Console.WriteLine("amount:" + outstanding);
}
```

```csharp {6,9-13|*}
// step 2
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
