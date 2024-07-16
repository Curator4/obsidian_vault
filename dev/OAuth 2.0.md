tags: [[authorization]], [[web]]

Log in with twitter, google, facebook = oauth2.

Commonly used to grant permissions for applications to access user information without passwords.

OAuth 2 is still an open standard, so each API will have its own flow based on its particular implementation.

Authentication in OAuth is facilitated by the use of _access tokens_.

## Roles

- **Resource Owner**: An entity capable of granting access to a protected resource. It could be a system or an end-user.
- **Client**: An application making protected resource requests on behalf of the Resource Owner and with its authorization.
- **Authorization Server**: The server that issues access tokens to the client after successfully authenticating the resource owner and obtaining authorization. The authorization server exposes two endpoints: the Token endpoint, which is involved in a machine-to-machine interaction for issuing access tokens, and the Introspection endpoint, which is used by the Resource Server to validate client access tokens.
- **Resource Server**: The server protecting the user resources capable of accepting and responding to protected resource requests using access tokens. In this guide, NGINX running within the API Connectivity Manager API-Proxy is the Resource Server.

### Photo example:
![[Pasted image 20231123184149.png]]