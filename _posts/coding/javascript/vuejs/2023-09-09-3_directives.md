---
layout: post
title: 'VueJS Directives'
date: 2023-09-09 22:03:00 +0200
categories: VueJs
author: 'Daria Graf'
---

# Directives

## v-for

```html
<ul>
  <child-component v-for="child in childs" :key="child.id" :name="child.name">
  </child-component>
</ul>
```
