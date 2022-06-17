---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---

# Collaboration = 
# Svelte Stores + CRDTs

Svelte Writable Derived Stores, Yjs, Websockets

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: image-right
image: https://images.unsplash.com/photo-1527525443983-6e60c75fff46?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=685&q=80
---

# Y Collaboration & Cooperation?

### Philosophical

"The Sapiens secret of success is large-scale flexible cooperation" - Yuval Noah Harari

So... Let's build more **"vast networks of cooperation"**
  
<br>

### Real World

- **[Google Docs](https://docs.google.com)** - Collaborative Editing of sheets, docs, drawings
- **[Miro](https://www.miro.com)** - Infinite canvas which supports video, diagrams, and many elements
  
<br>
<br>





<!--
Collaboration - the action of working with someone to produce something.
Cooperation - the action or process of working together to the same end.

"This has made us masters of the world. But at the same time it has made us dependent for our very survival on vast networks of cooperation."
-->

---

# Our Application Requirements

### Collaboration that we needed

- **Visual**
- **Component**
- **JSON**

<img src="data:image/png;base64,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
">

<!--
- **Visual** - Moving elements on the canvas moves in realtime
- **Component** - Adding, removing elements to the canvas
- **JSON** - Advanced JSON document editing in tree and code mode
-->

---

# Code

Use code snippets and get the highlighting directly![^1]

```ts {all|2|1-6|9|all}
interface User {
  id: number
  firstName: string
  lastName: string
  role: string
}

function updateUser(id: number, update: User) {
  const user = getUser(id)
  const newUser = { ...user, ...update }
  saveUser(id, newUser)
}
```

<arrow v-click="3" x1="400" y1="420" x2="230" y2="330" color="#564" width="3" arrowSize="1" />

[^1]: [Learn More](https://sli.dev/guide/syntax.html#line-highlighting)

<style>
.footnotes-sep {
  @apply mt-20 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>

---

# Components

<div grid="~ cols-2 gap-4">
<div>

You can use Vue components directly inside your slides.

We have provided a few built-in components like `<Tweet/>` and `<Youtube/>` that you can use directly. And adding your custom components is also super easy.

```html
<Counter :count="10" />
```

<!-- ./components/Counter.vue -->
<Counter :count="10" m="t-4" />

Check out [the guides](https://sli.dev/builtin/components.html) for more.

</div>
<div>

```html
<Tweet id="1390115482657726468" />
```

<Tweet id="1390115482657726468" scale="0.65" />

</div>
</div>


---
class: px-20
---

# Themes

Slidev comes with powerful theming support. Themes can provide styles, layouts, components, or even configurations for tools. Switching between themes by just **one edit** in your frontmatter:

<div grid="~ cols-2 gap-2" m="-t-2">

```yaml
---
theme: default
---
```

```yaml
---
theme: seriph
---
```

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-default/01.png?raw=true">

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-seriph/01.png?raw=true">

</div>

Read more about [How to use a theme](https://sli.dev/themes/use.html) and
check out the [Awesome Themes Gallery](https://sli.dev/themes/gallery.html).

---
preload: false
---

# Animations

Animations are powered by [@vueuse/motion](https://motion.vueuse.org/).

```html
<div
  v-motion
  :initial="{ x: -80 }"
  :enter="{ x: 0 }">
  Slidev
</div>
```

<div class="w-60 relative mt-6">
  <div class="relative w-40 h-40">
    <img
      v-motion
      :initial="{ x: 800, y: -100, scale: 1.5, rotate: -50 }"
      :enter="final"
      class="absolute top-0 left-0 right-0 bottom-0"
      src="https://sli.dev/logo-square.png"
    />
    <img
      v-motion
      :initial="{ y: 500, x: -100, scale: 2 }"
      :enter="final"
      class="absolute top-0 left-0 right-0 bottom-0"
      src="https://sli.dev/logo-circle.png"
    />
    <img
      v-motion
      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }"
      :enter="final"
      class="absolute top-0 left-0 right-0 bottom-0"
      src="https://sli.dev/logo-triangle.png"
    />
  </div>

  <div
    class="text-5xl absolute top-14 left-40 text-[#2B90B6] -z-1"
    v-motion
    :initial="{ x: -80, opacity: 0}"
    :enter="{ x: 0, opacity: 1, transition: { delay: 2000, duration: 1000 } }">
    Slidev
  </div>
</div>

<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->
<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  rotate: 0,
  scale: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

<div
  v-motion
  :initial="{ x:35, y: 40, opacity: 0}"
  :enter="{ y: 0, opacity: 1, transition: { delay: 3500 } }">

[Learn More](https://sli.dev/guide/animations.html#motion)

</div>

---

# LaTeX

LaTeX is supported out-of-box powered by [KaTeX](https://katex.org/).

<br>

Inline $\sqrt{3x-1}+(1+x)^2$

Block
$$
\begin{array}{c}

\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} &
= \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\

\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\

\nabla \cdot \vec{\mathbf{B}} & = 0

\end{array}
$$

<br>

[Learn more](https://sli.dev/guide/syntax#latex)

---

# Diagrams

You can create diagrams / graphs from textual descriptions, directly in your Markdown.

<div class="grid grid-cols-3 gap-10 pt-4 -mb-6">

```mermaid {scale: 0.5}
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```

```mermaid {theme: 'neutral', scale: 0.8}
graph TD
B[Text] --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

```plantuml {scale: 0.7}
@startuml

package "Some Group" {
  HTTP - [First Component]
  [Another Component]
}

node "Other Groups" {
  FTP - [Second Component]
  [First Component] --> FTP
}

cloud {
  [Example 1]
}


database "MySql" {
  folder "This is my folder" {
    [Folder 3]
  }
  frame "Foo" {
    [Frame 4]
  }
}


[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml
```

</div>

[Learn More](https://sli.dev/guide/syntax.html#diagrams)


---
layout: center
class: text-center
---

# Learn More

[Documentations](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)
