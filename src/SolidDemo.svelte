<script>
    import { fetch } from '@inrupt/solid-client-authn-browser';

    let data;
    let resource = "https://hochstenbach.inrupt.net/private/";

    async function handleFetch() {
        const response = await fetch(resource, { 
                          headers: new Headers({ Accept: "text/turtle" }) 
                        });
        data = await response.text();
    }
</script>

<div>
  <input
    size="80"
    type="text"
    bind:value={resource}
  />
  <button on:click={handleFetch}>Fetch</button>
</div>
{#if data}
<textarea cols=86 rows=20>{data}</textarea>
{/if}