# Connect Apps to GitHub

## Prerequisite

1. Follow the [official guide](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app) to create a OAuth App.
2. In "Authorization callback URL", use `https://<YOUR_AUTHGEAR_ENDPOINT>/sso/oauth2/callback/github`.
3. After the creation, click "Generate a new client secret". Remember the client secret.

## Configure Sign in with GitHub through the portal

Go to "Single-Sign On" page, and do the following:

1. Enable "Sign in with GitHub"
2. Fill in "Client ID".
3. Fill in "Client Secret".
4. **Save** the changes.

🎉 Done! You have just added GitHub integration to your apps!
