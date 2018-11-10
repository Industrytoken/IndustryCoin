# Third party integrations

## Setup Github OAuth2 App Integration (Recommended)

Navigate to: [Github - New Application](https://github.com/settings/applications/new) and enter similar values to:

* Enter Application Name: `MyindustrycoinApp`
* Homepage URL: `http://localhost`
* Application description: `My industrycoin App`
* Authorization callback URL: `http://localhost:8000/` (required)

The authorization callback URL should match your `BASE_URL` value in `web/app/app/.env`

Update the `web/app/app/.env` file to include the values provided by Github:

```shell
GITHUB_CLIENT_ID=xxxx
GITHUB_CLIENT_SECRET=xxx
GITHUB_APP_NAME=MyindustrycoinApp
```

Please `docker-compose down; docker-compose up -d` to have the environment variable changes reflect in your local industrycoin environment.

## Setup Github User Integration (Recommended)

Navigate to: [Github - New Token](https://github.com/settings/tokens/new)
At minimum, select `user` scope.

Update the `web/app/app/.env` file to include the values provided by Github:

```shell
GITHUB_API_TOKEN=xxx
GITHUB_API_USER=xxx
```

Make sure you disable industrycoinbot notifications on your local, unless you are specifically testing that feature
By default, we disable outbound GitHub notifications to any repository that isn't under the `GITHUB_API_USER` repositories.

For example, if `settings.GITHUB_API_USER == industrycoinco` only `github.com/industrycoinco/<repos>` bounties and associated tips will post Github comments.

## Setup SendGrid to Send Emails (Recommended)

1. Create a new SendGrid Account at https://sendgrid.com
2. Go to [https://app.sendgrid.com/settings/api_keys](https://app.sendgrid.com/settings/api_keys) and create a new Sendgrid API key:

Update the `web/app/app/.env` file to include the values provided by Github:

```shell
SENDGRID_API_KEY=xxx
CONTACT_EMAIL=xxx
```

```
# Be VERY CAREFUL when changing this setting.  You don't want to accidently
# send a bunch of github notifications :)
ENABLE_NOTIFICATIONS_ON_NETWORK=None
```

## industrycoinbot Installation Instructions

### This integration requires the Github OAuth2 App Integration

Navigate to: [industrycoinbot Github App](https://github.com/apps/industrycoinbot)
Copy the application ID found on the page as the `industrycoinBOT_APP_ID` environment variable.

Make sure you disable industrycoinbot notifications on your local, unless you are specifically testing that feature

```
# Be VERY CAREFUL when changing this setting.  You don't want to accidentally
# send a bunch of github notifications :)
ENABLE_NOTIFICATIONS_ON_NETWORK=None
```

The following environment variables must be set for industrycoinbot to work correctly:

```shell
GITHUB_API_USER=industrycoinbot  # Github Profile name of the bot. Defaults to: industrycoinbot
industrycoinBOT_APP_ID=APP_ID_FROM_ABOVE  # Defaults to empty.
industrycoin_BOT_CERT_PATH=RELATIVE_PATH_TO_CERT_FILE  # Defaults to empty.
```

#### Example

```shell
GITHUB_API_USER=industrycoinbot  # Github Profile name of the bot. Defaults to: industrycoinbot
industrycoinBOT_APP_ID=7735  # industrycoin Bot App ID
industrycoin_BOT_CERT_PATH=app/industrycoin_bot_secret.pem  # If pem file is located at web/app/app/industrycoin_bot_secret.pem
```

Aside from these environment variables, the settings page of the industrycoin bot application must have the correct url for webhook events to post to. It should be set to `https://idtoken.pro/payload` based on urls.py line 131.

After running the migrations and deploying the idtoken.pro website, industrycoinbot will begin to receive webhook events from any repository that it is installed into. This application will then parse through the comments and respond if it is called with @industrycoinbot + registered action call.

## Sentry Integration

Error tracking is entirely optional and primarily for internal staging and production tracking.
If you would like to track errors of your local environment, setup an account at: [Sentry.io](https://sentry.io)

Once you have access to your project secrets, you can enable Sentry error tracking for both the backend and frontend by adding the following environment variables to `web/app/app/.env`:

```shell
SENTRY_USER=xxx
SENTRY_PASSWORD=xxx
SENTRY_ADDRESS=https://sentry.example.xxx
SENTRY_PROJECT=2
```
