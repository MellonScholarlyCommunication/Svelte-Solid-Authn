<script>
    import { handleIncomingRedirect, login, logout, getDefaultSession } from '@inrupt/solid-client-authn-browser';
    import { session } from './session';

    export let webId;
    export let issuer;

    handleIncomingRedirect({
        restorePreviousSession: true,
        onError: (error, errorDescription) => {
            console.log(`${error} has occured: `, errorDescription);
        }
    }).then((info) => {
        webId = info.webId;
        session.set( getDefaultSession() );
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
        console.debug(`Logout from : ${issuer}`);
        logout();
        webId = undefined;
        session.set(undefined);
    }
</script>

<div>
    <form>
      IDP:
      <input
        size="40"
        type="text"
        bind:value={issuer}
      />
      <button on:click|preventDefault={handleLogin}>Log In</button>
      <button on:click|preventDefault={handleLogout}>Log Out</button>
    </form>
</div>