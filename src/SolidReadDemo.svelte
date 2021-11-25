<script>
    import { fetch } from '@inrupt/solid-client-authn-browser';
    import { session } from './session.js';

    export let resource;

    let value;
    let info;

    // When we are logged in we get a fresh session object
    session.subscribe( s => {
        if (s) {
          info = s.info;
        }
        else {
          info = undefined;
        }
    });

    async function handleFetch() {
        const response = await fetch(resource, { 
                          headers: new Headers({ Accept: "text/turtle" }) 
                        });
        value = await response.text();
    }
</script>

<h2>Read demo</h2>
{#if info && info.isLoggedIn}
  <div>
      <input
       size="80"
       type="text"
       bind:value={resource}
  />
      <button on:click={handleFetch}>Fetch</button>
  </div>
  {#if value}
    <textarea id="demoReadText" cols=86 rows=20 bind:value></textarea>
  {/if}
{:else}
  <p>Not logged in</p>
{/if}