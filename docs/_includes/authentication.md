## Audience

This is aimed at NetFoundry customers and [trial users](https://nfconsole.io/signup) who will use the API directly to augment and automate their use of the NF Console.

RapidAPI subscribers will use their RapidAPI token with the RapidAPI code samples instead of an Auth0 credential.
{: .notice--warning}

## Overview

All authenticated operations require an HTTP header like

```http
Authorization: Bearer {NETFOUNDRY_API_TOKEN}
```

where `{NETFOUNDRY_API_TOKEN}` is an expiring JSON Web Token (JWT) that you obtain from Auth0, NetFoundry API's identity provider, by authenticating with your permanent credential.

## Shell example

Pull it all together with [HTTPie (command-line HTTP client)](https://httpie.org/) and [`jq` (command-line JSON processor)](https://stedolan.github.io/jq/).

```bash
source export-netfoundry-api-token.bash
```

[download this example](/assets/export-netfoundry-api-token.bash)

{% highlight bash %}
{% include export-netfoundry-api-token.bash %}
{% endhighlight %}

## Step by Step

### Get a permanent credential

1. [Start a free trial](https://nfconsole.io/signup) if you need a login for NF Console
2. [Log in to NF Console](https://nfconsole.io/login)
3. In NF Console, navigate to "Organization", "Manage API Account", and click <i class="fas fa-plus-circle"></i>

### Get a temporary token

Use your permanent credential; `client_id`, `client_secret`; to obtain an expiring `access_token` from the identity provider, Auth0. Here are examples for `curl` and `http` to get you started.

**HTTPie**

```bash
❯ http POST https://netfoundry-production.auth0.com/oauth/token \
  "client_id=${NETFOUNDRY_CLIENT_ID}" \
  "client_secret=${NETFOUNDRY_CLIENT_SECRET}" \
  "audience=https://gateway.production.netfoundry.io/" \
  "grant_type=client_credentials"
```

**cURL**

```bash
❯ curl \
    --silent \
    --show-error \
    --request POST \
    --header 'content-type: application/json' \
    --data '{
        "client_id": "'${NETFOUNDRY_CLIENT_ID}'",
        "client_secret": "'${NETFOUNDRY_CLIENT_SECRET}'",  
        "audience": "https://gateway.production.netfoundry.io/",
        "grant_type": "client_credentials"
    }' \
    https://netfoundry-production.auth0.com/oauth/token
```
