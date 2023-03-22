---
title:  'What am I reading?'
author: 'Shana'
keywords: [reading]
---

<div id="observablehq-52db9cf9">
  <div class="observablehq-books2"></div>
</div>
<script type="module">
  import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@4/dist/runtime.js";
  import define from "https://api.observablehq.com/@shanamatthews/spine-generator-open-library-edition.js?v=3";
  (new Runtime).module(define, name => {
    if (name === "books2") return Inspector.into("#observablehq-52db9cf9 .observablehq-books2")();
  });
</script>

I made this with D3 on [Observable](https://observablehq.com/). I've written a couple posts about how I made it, but the best resource is the [Observable Notebook itself](https://observablehq.com/@shanamatthews/spine-generator-open-library-edition?collection=@shanamatthews/spine-generator) where I have quite a bit of explanation of what I did.

- [Switching from Goodreads to Open Library](../posts/goodreads-to-open-library.html)
- [Spine Generator Open Library Edition](../posts/spine-generator-open-library-edition.html)
