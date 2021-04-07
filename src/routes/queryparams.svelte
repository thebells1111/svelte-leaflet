<script context="module">
  import { writable } from "svelte/store";

  export async function load({ page }) {
    const { query } = page;
    const q = query.get("q") || "";
    console.log("load", { page })
    return {
      props: {
        q: writable(q),
        s: q,
        t: "I am a string",
        w: writable("Writable here 👋")
      },
    };
  }
</script>

<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  export let q = writable("");
  export let t = "";
  export let s = "";
  export let w = writable("");

  console.log("onmount", $page.query.toString())

  onMount(async () => {
    console.log("---");
    console.log($q);
    console.log(t);
    console.log(s);
    console.log($w);
    console.log("---");
    console.log("onmount", $page.query.toString())
    console.log("onmount q", $page.query.get("q"))
  });
</script>

<div>s: {s}</div>
<div>q: {$q}</div>
<div>t: {t}</div>
<div>w: {$w}</div>
