# Curling is Fun!

## Solution

Given the name of the challenge, I immediatly knew I had to curl into the website, so:

```bash
curl XXXXXX-curling-is-fun-web.chall.lilypadd.com
```

Just like that we get the first part of the **flag**. We also receive the following message:

> Send a POST request to / with the JSON data '{"hello": "world"}' to get the second half!

Translating that into curl:

```bash
curl -X POST -d '{"hello": "world"}' XXXXXX-curling-is-fun-web.chall.lilypadd.com
```

The response includes the second (and final) part of the **flag**.