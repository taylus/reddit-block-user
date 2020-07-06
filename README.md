# Block users on reddit

Without having to private message or report them.

## Who thought this was a good idea?

If you've ever visited <https://www.reddit.com/prefs/blocked>, you'll see this notice:

```plain
To block a user click 'block user' below a message from a user you wish to block from messaging you.
```

I don't think you should have to interact with someone to block them. [The reddit API doesn't, either](https://www.reddit.com/dev/api/#POST_api_block_user). But in a confusing display of poor user experience, this feature is (kind of?) missing from the UI.

When I say kind of, that's because you can (sometimes?) block someone by reporting their posts. But this isn't the case in the (otherwise great) [app I use on iOS](http://getnarwhal.com/), so I wrote this.

[Reddit Enhancement Suite](https://redditenhancementsuite.com/) also lets you block people, but this doesn't carry over to mobile.

## Blocking users using the reddit API

The following demonstrates how to use the reddit API to block users using an HTTP client such as `curl` or [Postman](https://www.postman.com/). Basic proficiency using REST APIs helps but is not required.

### Register a "script" type application for personal use

Follow [these instructions](https://github.com/reddit-archive/reddit/wiki/OAuth2-Quick-Start-Example) in order to create an "application" you can use to access the reddit API. Upon completion this will provide you a client ID and secret for use in subsequent API calls.

### Use the "password" grant type for quick n' dirty authentication

Send a `POST` request to `https://www.reddit.com/api/v1/access_token` with:

* The following `x-www-form-urlencoded` body:
  * `grant_type=password&username={username}&password={password}`
  * Where `{username}` and `{password}` are your reddit account username and password
* Your application's client ID and secret sent as Basic authentication headers
  * i.e. `Authorization Basic` + base64(clientId:clientSecret)

If successful, you should get a response back with an `access_token`, hang onto that for the next call.

### Block the user

Send a `POST` request to `https://oauth.reddit.com/api/block_user` with:

* A body conforming to the [documentation here](https://www.reddit.com/dev/api/#POST_api_block_user)
  * `account_id` and `uh` don't seem necessary?
  * I got by with just `api_type=json&name={name}`
  * Where {name} is the reddit username you wish to block

If successful, you should get an `HTTP 200 OK` response back w/ information about the block in the response body.

You can now confirm the block by going to <https://www.reddit.com/prefs/blocked>, or by making the [GET /prefs/blocked](https://www.reddit.com/dev/api/#GET_prefs_blocked) API call.

## Alternative browser dev tools-based approach

[From /u/Pokechu22](devtools-approach.md)

## TODO

* More user-friendly approach based on <https://github.com/reddit-archive/reddit/wiki/OAuth2#authorization>?

## References

* <https://www.reddit.com/dev/api/>
* <https://stackoverflow.com/questions/28955541/how-to-get-access-token-reddit-api/29038271#29038271>
