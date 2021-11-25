<script>
    import { fetch } from '@inrupt/solid-client-authn-browser';
    import { addUrl, createSolidDataset , createThing, setThing } from '@inrupt/solid-client';
    import { session } from './session.js';

    export let resource;

    let info;
    let value = `
PREFIX : <urn:x:base:> 

:a :b :c .
`;
    let status;

    // When we are logged in we get a fresh session object
    session.subscribe( s => {
       if (s) {
           info = s.info;
       }
       else {
           info = undefined;
       }
    });

    async function handleWrite() {
        const response = await fetch(resource, { 
                          headers: new Headers({ 'Content-Type': 'text/turtle' })  ,
                          method: 'PUT' ,
                          body: value
                        });
        status = response.statusText;
    }
</script>

<h2>Write demo</h2>
{#if info && info.isLoggedIn}
    {#if status}
    <p>Response: {status}</p>
    {/if}
    <div>
       <input
        size="80"
        type="text"
        bind:value={resource}
        />
    <button on:click={handleWrite}>Update</button>
    </div>
    <textarea id="demoWriteText" cols=86 rows=20 bind:value></textarea>
{/if}