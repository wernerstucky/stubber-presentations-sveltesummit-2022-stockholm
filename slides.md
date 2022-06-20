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
download: true
# some information about the slides, markdown enabled
info: |
  ## Svelte Summit 2022 Stockholm - Werner Stucky Stubber.com
# persist drawings in exports and build
drawings:
  persist: false
#testing 123
#Diagram at : https://docs.google.com/drawings/d/18Zx6BLsr5Ay_jCoxsNwV6r4pNMgMh9Ng7iv3ulzobhM/edit
layout: cover
background: https://images.unsplash.com/photo-1581007156996-99fe0ece1d9c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1332&q=80
---

# Collaboration = 
# Svelte Stores + CRDTs

Svelte Writable Derived Stores, Yjs, Websockets

By Werner Stucky - CEO Stubber.com

# DRAFT - DRAFT - DRAFT

<div class="pt-12">
  <a href="[link to live slides]">Live Link</a>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/wernerstucky/stubber-presentations-sveltesummit-2022-stockholm" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--


-->

---
layout: image-right
image: https://images.unsplash.com/photo-1527525443983-6e60c75fff46?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=685&q=80
---

# Why? Collaboration & Cooperation

<div v-click>

### Philosophical

"The Sapiens secret of success is large-scale flexible cooperation" - Yuval Noah Harari

So... Let's build more **"vast networks of cooperation"**
  
<br>

</div>

<div v-click>

### Real World

- **<logos-google-drive/> [Google Docs](https://docs.google.com)** -  Collaborative Editing of sheets, docs, drawings
- **[Miro](https://www.miro.com)** - Infinite canvas which supports video, diagrams, and many elements
  
</div>



<!--
Collaboration - the action of working with someone to produce something.
Cooperation - the action or process of working together to the same end.
Coordination - the organization of the different elements of a complex body or activity so as to enable them to work together effectively.

"This has made us masters of the world. But at the same time it has made us dependent for our very survival on vast networks of cooperation."

**Real World**

If you've ever worked on Google Sheets and then have had to revert to working with someone on a version of Excel that gets mailed back and forth you'll know
-->

---

# What we set out to build

### Visual Flow Editor based on JSPlumb

<img  src="/floweditor.png" class="m-5 h-60 rounded shadow" >

<logos-github-icon/><a href="https://github.com/jsplumb/jsplumb">https://github.com/jsplumb/jsplumb</a>



<!--
- **Visual** - Moving elements on the canvas moves in realtime
- **Component** - Adding, removing elements to the canvas
-->

---

# What we set out to build

### JSON Editor live editing

<img  src="/jsoneditor.png" class="m-5 h-60 rounded shadow" >

<logos-github-icon/><a href="https://github.com/josdejong/svelte-jsoneditor">https://github.com/josdejong/svelte-jsoneditor</a>


<!--
- **JSON** - Advanced JSON document editing in tree and code mode
-->


---

# CRDTs

CRDT || OT (Operational Transform)

https://josephg.com/blog/crdts-are-the-future/

"So that means we’ve made CRDTs good enough that the difference in speed between CRDTs and OT is smaller than the speed difference between Rust and Javascript."


Conflict-free Replicated Data Types



  - Delivered reliably and in casual order



### Different types of CRDT Types

  - Array
  - Map
  - Text



<!--

  - Not going into details, many others have done a really good job
  - See resources slide


** Ways of thinking of it **

  - A place you send all changes to get out the central truth
  - A central vote counting location that collects votes from all the polling stations and outputs a summary vote
  - The person that stands at the watercooler and collects all the gossip and rebroadcasts the final updated version to everyone
  - 





-->



---

# SyncedStore Code

store.js
```js {all|1|2|3|7|13|all}
import { syncedStore, getYjsValue } from "@syncedstore/core";
import { WebrtcProvider } from "y-webrtc";
import { svelteSyncedStore } from "@syncedstore/svelte";

// Create your SyncedStore store
export const store = syncedStore({
	template:{}
});
export const svelteStore = svelteSyncedStore(store);

// Create a document that syncs automatically using Y-WebRTC
const doc = getYjsValue(store);
export const webrtcProvider = new WebrtcProvider("syncedstore-werner-sveltesummit-demo", doc);

export const disconnect = () => webrtcProvider.disconnect();
export const connect = () => webrtcProvider.connect();
```


---

# SyncedStore Code

App.svelte
```html {all|2|17|16|6|all}
<script>
	import { svelteStore } from "./store.js";
	import { JSONEditor } from 'svelte-jsoneditor';
	
	function setInitialContent(){
		$svelteStore.template.editor = {
			"json":{
				"name":"werner"
			}
		};
	}//setContent
</script>

<main id="app">
	<h1>JSON Editing</h1>
	<button on:click={setInitialContent}>Set Initial Content</button>
	<JSONEditor bind:content={$svelteStore.template.editor} />
</main>
```

---

# Demo

[Svelte REPL](https://svelte.dev/repl/1d8ea22b226d481882a2a652f381ffc1?version=3.48.0)

---
layout: center
class: text-center
---


## CRDT

[CRDT Tech](https://crdt.tech)


## OT

https://github.com/share/sharedb






