# Sentry

## Installation

### Next.js

#### Instructions

Integrating Sentry in an (existing) Next.js application. Before starting make sure that you created a project in Sentry. Then follow the wizard provided by running the following command.

```
npm install --save @sentry/nextjs
```

Next, run the following command to start the wizard.

```
npx @sentry/wizard -i nextjs
```

Follow the wizard and select the right project. This should place multiple files in your Next.js project.&#x20;

* `sentry.client.config.js`, `sentry.edge.config.js` and `sentry.server.config.js` these files initialise Sentry.
* `next.config.js` with additonal configurations. The original `next.config.js` is placed in a file with a similar name. Please check this one and merge it with the `next.config.js` and remove the file.
* `sentry.properties` this file includes the configuration for sentry-cli. This file can be savely added to VC.
* `.sentryclirc` the token included in this file can be moved to the .env file using the `SENTRY_AUTH_TOKEN` variable.
* `pages/api/error.ts` and `pages/sentry_test_error.tsx`. These files can be used to test whether Sentry has been setup properly.

When setup correctly you can head to Sentry to see potential errors. The `NODE_ENV` variable is used to create the different environments. Furthermore it could be useful to upload source maps which can be done conventionally using an integration with most hosting providers, e.g. Heroku or Vercel.&#x20;

#### Resources

* [https://docs.sentry.io/platforms/javascript/guides/nextjs/](https://docs.sentry.io/platforms/javascript/guides/nextjs/)
* [https://www.youtube.com/watch?v=tLvpZQI\_qjE](https://www.youtube.com/watch?v=tLvpZQI\_qjE)
*
