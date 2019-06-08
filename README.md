<div align="center">
<img src="https://user-images.githubusercontent.com/26399680/59146646-5e2ce600-8a23-11e9-9c2c-46465b18e06f.png" width="80%">

<h1> Bannero API </h1>
<p>🚀🥇🗳</p>

<strong><p> Simple random banner pictures for blogs, websites and more.</p></strong>


</div>

## About

Another way to implement [spencerwooo/bannero](https://github.com/spencerwooo/bannero) API service

Just for seeking a new free approach to host an redirect server

Powered by [Cloudflare Worker®](https://workers.cloudflare.com/docs)

*Workers Free plan Includes 100,000 total requests per day*

## Deployment

I think this simple code do not need the help of [wrangler CLI tool](https://github.com/cloudflare/wrangler) and webpack

Only 3 steps:

1. Goto the Cloudflare Worker® DashBoard
2. Create a new script with the following code
3. Add a route and deploy it

```javascript
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

const handleRequest = async request => {
  let list = await bannero(request)
  let choice = crypto.getRandomValues(new Uint16Array(1))[0] % list.length
  return Response.redirect(list[choice], 302)
}

const bannero = async () => {
  let remote = await fetch('https://raw.githubusercontent.com/spencerwooo/bannero/master/src/bannero.txt', {cf: {cacheEverything: true}})
  let text = await remote.text()
  return text.split('\n').slice(1, -1)
}
```

> The code will be deployed to hundreds of data centers around the world returning responses to your users faster than your origin ever could. You get all the speed and security of the world’s most peered CDN with all the power of JavaScript.

## Reference

- [spencerwooo/bannero](https://github.com/spencerwooo/bannero)

## License

MIT
