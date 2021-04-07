<script context="module">
  export async function load({page}) {
    console.log({page})
    return {
      props: {
        query: page.query
      }
    }
  }
</script>

<a href="https://github.com/sveltejs/kit/issues/631" target="_blank">Issue 631</a>
