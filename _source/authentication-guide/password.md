---
layout: docs_page
title: Implementing the Resource Owner Password Flow
excerpt: How to implement the resource owner password flow in Okta
---

# Implementing the Resource Owner Password Flow

The Resource Owner Password Flow is intended for use cases where you control both the client application and the resource that it is interacting with. At a high-level, this flow has the following steps:

- Your client application collects a user's credentials
- Your application sends these credentials to your Okta authorization server
- If the credentials are accurate, Okta responds with the requested tokens

For more information on the resource owner password flow, including why to use it, see (jakub.todo).

### 1. Setting up your Application

1. From the Applications page, choose **Add Application**
2. You will now be on the Create New Application page. From here, select **Native**
3. Fill-in the Application Settings, being sure to select "Resource Owner Password" as one of the allowed grant types, then click **Done**.
4. On the next screen, in the "Client Credentials section", click **Edit**.
5. Select "Use Client Authentication", then click **Save**.

### 2. Using the Resource Owner Password Flow

Before you can begin this flow, you will have to collect the user's password in a manner of your choosing. 

Once you have collected the credentials, all that is required is a single API call to the `/token` endpoint:

```
curl --request POST \
  --url https://dev-686102.oktapreview.com/oauth2/default/v1/token \
  --header 'accept: application/json' \
  --header 'authorization: Basic MG9hYnpsamloM3JucjZhR3QwaDc6UHU4X2hmQkxzOGxNejVnMTZBNllmY0xid091LTExOFRPNF9YR1VOTQ==' \
  --header 'cache-control: no-cache' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data 'grant_type=password&redirect_uri=http%3A%2F%2Flocalhost&username=testuser1%40example.com&password=%7CmCovrlnU9oZU4qWGrhQSM%3Dyd&scope=openid'
```

> Note: The call to the `/token` endpoint requires authentication. For more on this, please see [Token Authentication Methods](https://developer.okta.com/docs/api/resources/oauth2.html#token-authentication-methods).

If the credentials are valid, your application will receive back access and ID tokens:

```
{
    "access_token": "eyJhb[...]56Rg",
    "expires_in": 3600,
    "id_token": "eyJhb[...]yosFQ",
    "scope": "openid",
    "token_type": "Bearer"
}
```

### 3. Next Steps

When your application passes a request with an access_token, the resource server will need to validate it. For more on this, see (jakub.todo).

### 4. Samples