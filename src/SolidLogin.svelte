<script>
    import { handleIncomingRedirect, login, logout, fetch, getDefaultSession } from '@inrupt/solid-client-authn-browser'

    let webId    = getDefaultSession().info.webId;
    let issuer   = "https://hochstenbach.inrupt.net";
    let resource = "https://hochstenbach.inrupt.net/private/";
    let data     = "";

    handleIncomingRedirect({
        restorePreviousSession: true,
        onError: (error, errorDescription) => {
            console.log(`${error} has occured: `, errorDescription);
        }
    }).then((info) => {
        webId = info.webId;
    });
   
    function handleLogin() {
        console.debug(`Login to : ${issuer}`);
        login({
            redirectUrl: process.env.REDIRECT_URL,
            oidcIssuer: issuer,
            clientName: "Demo app"
        });
    }

    function handleLogout() {
        logout();
        webId = undefined;
    }

    async function handleFetch() {
        const response = await fetch(resource, { 
                          headers: new Headers({ Accept: "text/turtle" }) 
                        });
        data = await response.text();
    }
</script>

<p>{webId ? `Logged in as ${webId}` : "Not logged in yet"}</p>

<div>
    <form>
      <input
        type="text"
        bind:value={issuer}
      />
      <button on:click|preventDefault={handleLogin}>Log In</button>
      <button on:click|preventDefault={handleLogout}>Log Out</button>
    </form>
</div>

<hr />
<div>
  <input
    size="80"
    type="text"
    bind:value={resource}
  />
  <button on:click={handleFetch}>Fetch</button>
</div>
<textarea cols=86 rows=20>{data}</textarea>