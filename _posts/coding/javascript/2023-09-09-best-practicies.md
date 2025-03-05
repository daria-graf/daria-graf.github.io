---
layout: post
title: 'Best practicies'
date: 2023-09-09 21:17:00 +0200
categories: javascript
author: 'Daria Graf'
---

# Returning Boolean Values from Functions

```js
function isEqual(a, b) {
  if (a === b) {
    return true;
  } else {
    return false;
  }
}
```

Better

```js
function isEqual(a, b) {
  return a === b;
}
```
