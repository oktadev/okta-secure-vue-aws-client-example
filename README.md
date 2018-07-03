# A Secure Vue.js App, Deployed to AWS
 
This example app shows how to build a Vue.js app, deploy it to AWS, add CloudFront as a CDN, and deploy an Express API to AWS Lambda.

Please read [Deploy Your Secure Vue.js App to AWS](https://developer.okta.com/blog/2018/07/03/deploy-vue-app-aws) to see how this app was created.

**Prerequisites:** [Node.js](https://nodejs.org/).

> [Okta](https://developer.okta.com/) has Authentication and User Management APIs that reduce development time with instant-on, scalable user infrastructure. Okta's intuitive API and expert support make it easy for developers to authenticate, manage, and secure users and roles in any application.

* [Getting Started](#getting-started)
* [Links](#links)
* [Help](#help)
* [License](#license)

## Getting Started

To install this example application, run the following commands:

```bash
git clone https://github.com/oktadeveloper/okta-secure-vue-aws-client-example.git vue-aws-client
cd vue-aws-client
```

This will get a copy of the project installed locally. To install all of its dependencies and start the app, run the commands below.

```
npm install
npm run dev
```

You will also need to get the server example app if you want to verify API communication works.

```bash
git clone https://github.com/oktadeveloper/okta-secure-vue-aws-server-example.git vue-aws-server
cd vue-aws-server
npm install
```

### Setup Okta

To use Okta, you'll need to change a few things. First, you'll need to create a free developer account at <https://developer.okta.com/signup/>. After doing so, you'll get your own Okta domain, that has a name like `https://dev-123456.oktapreview.com`.

Create an OIDC App in Okta to get a `{clientId}` and `{clientSecret}`. To do this, log in to your Okta Developer account and navigate to **Applications** > **Add Application**. Click **Single-Page App** and click the **Next** button. Give the app a name you’ll remember, specify `http://localhost:8080` as a Base URI, and `http://localhost:8080/implicit/callback` as a Login Redirect URI. Click **Done** and copy the client ID and secret into the files listed below.

**TIP:** You'll need to add a Login Redirect URI that matches your CloudFront URI after you've set that up. If you follow the steps in [this example's blog post](https://developer.okta.com/blog/2018/07/03/deploy-vue-app-aws), you'll have this information before you create your app in Okta.

Modify `vue-aws-client/src/router/index.js` to use your Okta settings.

```js
Vue.use(Auth, {
  issuer: 'https://{yourOktaDomain}/oauth2/default',
  client_id: '{clientId}',
  redirect_uri: window.location.origin + '/implicit/callback',
  scope: 'openid profile email'
})
```

Modify `vue-aws-server/app.js` too:

```js
const oktaJwtVerifier = new OktaJwtVerifier({
  clientId: '{clientId}',
  issuer: 'https://{yourOktaDomain}/oauth2/default'
})
```

## Links

This example uses the following open source libraries provided by Okta:

* [Okta Vue SDK](https://github.com/okta/okta-oidc-js/tree/master/packages/okta-vue)
* [Okta JWT Verifier for Node.js](https://github.com/okta/okta-oidc-js/tree/master/packages/jwt-verifier)

## Help

Please post any questions as comments on the [blog post](https://developer.okta.com/blog/2018/07/03/deploy-vue-app-aws), or visit our [Okta Developer Forums](https://devforum.okta.com/). You can also email developers@okta.com if would like to create a support ticket.

## License

Apache 2.0, see [LICENSE](LICENSE).
