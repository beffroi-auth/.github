# The OpenID Connect provider that PHP world deserves

On the map of a Symfony application, the interface is Symfony, the API is API Platform, and the identity provider is always somewhere else: Keycloak, Auth0, Entra. Beffroi is that provider, written in PHP: OAuth 2.0, OpenID Connect and SAML 2.0 on a pure-PHP core, under MIT.

It runs as an application of its own, beside the applications it signs people in to. They are its clients and talk to it through the protocols; none of them installs it. A deployment is one image, `ghcr.io/beffroi-auth/beffroi`: Symfony on FrankenPHP, PostgreSQL behind it, set by its environment.

## What it serves

| | |
|---|---|
| **Sign-in** | Passwords with typed hashes, passkeys as a first factor, TOTP and backup codes, `acr` and `amr` that say what was proved |
| **OAuth 2.0 and OpenID Connect** | Authorization code with PKCE `S256`, refresh tokens, client credentials, device code, CIBA, token exchange, JWT bearer; introspection, revocation, discovery, UserInfo, dynamic client registration, pairwise subjects |
| **FAPI 2.0** | Pushed authorization requests, signed request objects, signed authorization responses, DPoP and mutual TLS, tokens encrypted to the client |
| **Logout** | RP-initiated, front-channel and back-channel |
| **SAML 2.0** | The identity provider of the applications that speak SAML, and the service provider of the identity provider of an organisation, with single logout |
| **Keys** | The keys of each tenant sealed by a key management service: a sodium key, Vault Transit or AWS KMS |
| **Administration** | An administration API, and a terminal client that uses it |

## Secure by default

There is no option to do it wrong: no implicit flow, no password grant, PKCE with `S256` only, redirect URIs compared exactly, `iss` in every authorization response. Where an exception is unavoidable, it is named, carried by one client, and bounded.

## Judged from outside

The certification plans of the OpenID Foundation conformance suite run against the provider in continuous integration, in strict mode: Basic, Config and Form Post OP; RP-Initiated, Front-Channel and Back-Channel Logout; FAPI 2.0 Security and Signing, with DPoP and with mutual TLS; FAPI-CIBA; Dynamic OP, Third Party-Init OP and Rotate Keys. Symfony's own `oidc_login` client consumes the provider without a patch.

SAML 2.0 has no certification programme, so its judges are tools and implementations that are not ours: xmlsec1, SimpleSAMLphp, Microsoft Entra ID and Keycloak.

Beffroi is not OpenID Certified. Running the suite and holding the mark are two different things.

## Where things stand

Beffroi is 0.x until its 1.0, which ships with Symfony 8.4. Until then the public API may change between minor versions, and only the latest release is supported. It requires PHP 8.4 and Symfony 8.2.

## Where to find it

- **The code** is one monorepo, [beffroi-auth/beffroi](https://github.com/beffroi-auth/beffroi), where issues and pull requests go. Each package is mirrored, read only, into a repository of its own.
- **The documentation** is [doc.beffroi.tech](https://doc.beffroi.tech), written in [beffroi-auth/docs](https://github.com/beffroi-auth/docs).
- **A vulnerability** is reported privately, through the [security advisories](https://github.com/beffroi-auth/beffroi/security/advisories/new) of the monorepo.

## The name

A belfry is the tower a town built for itself: the bells that said what was happening, and the chest where the charter was kept. It watched over the town without owning it, which is the job of a piece of software standing at the door.
