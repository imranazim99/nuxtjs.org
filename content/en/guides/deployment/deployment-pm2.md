---
title: Deploy Nuxt using PM2
description: How to deploy Nuxt.js with PM2 cluster mode enabled?
menu: PM2
target: Server
category: deployment
position: 114
---

Deploying using [PM2](https://pm2.keymetrics.io/) (Process Manager 2) is a fast and easy solution for hosting your universal Nuxt application on your server or VM.

In this guide, we build the application locally and serve it though a PM2 config file with the cluster mode activated. Cluster mode will prevent downtime by allowing applications to be scaled across multiple CPUs.

## Getting Started

Make sure you have pm2 installed on your server. If not, simply globally install it from yarn or npm.

```bash
# yarn pm2 install
$ sudo yarn global add pm2 --prefix /usr/local

# npm pm2 install
$ npm install pm2 -g
```

## Configure your application

All you need to add to your universal Nuxt app for serving it though PM2 is a file called `ecosystem.config.js`. Create a new file with that name in your root project directory and add the following content:

```javascript
module.exports = {
  apps: [
    {
      name: 'NuxtAppName',
      exec_mode: 'cluster',
      instances: 'max', // Or a number of instances
      script: './node_modules/nuxt/bin/nuxt.js',
      args: 'start'
    }
  ]
}
```

## Build and serve the app

Now build your app with `npm run build`.

And serve it with `pm2 start`.

Check the status `pm2 ls`.

Your Nuxt.js application is now serving!

After `npm run build`, and then run `pm2 start` and my nuxt app is running on port then it tries to run app again and again and it throws error that app is already listening on port. While my `ecosystem.config.js` file is in fork mode.

## Further Information

This solution guarantees no downtime for your application on this server. (You should also prevent server failure through redundancy or high availability cloud solutions.)

You can find PM2 additional configurations [here](https://pm2.keymetrics.io/docs/usage/application-declaration/#general).