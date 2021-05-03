this is how you add a post:

`hugo new posts/my-first-post.md`

this is how you add a page to sidebar:
(this is what worked, but not necessarily, like the only way")

`hugo new pages/til_2021.md`

then in the title, add the menu field and update the name

```
---
title: "Things I've Learned"
date: 2021-05-03T11:50:12-07:00
draft: false
menu: "main"
weight: 300
---
```
