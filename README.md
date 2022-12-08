# Parse Server Starter

# Local Development (Docker)
```
cp .env.dev .env
docker compose up -d
npm i
npm start
```
## quick links

### parse server url
> [http://localhost:1337/parse/health](http://localhost:1337/parse/health)

### parse server dashboard
> [http://localhost:4040/](http://localhost:4040/)

# Local Development

1. Make sure you have a compatible Node.js version installed. Run `node --version` to see your local Node.js version. Open the `package.json` file too see which version of Node.js this example repository requires at `{ engines": { "node": "<NODE_VERSION>" } }`. Note that there may be other Parse Server version available that support older or newer Node.js versions, see the [Parse Server compatibility table](https://github.com/parse-community/parse-server#compatibility).
2. Clone this repository and change directory to it.
3. Run `npm install`.
4. Install a MongoDB database locally from https://docs.mongodb.org/master/tutorial/install-mongodb-on-os-x.
5. Run `mongo` to connect to your database, just to make sure it's working. Once you see a mongo prompt, exit with `Control-D`.
6. Launch Parse Server with `npm start`.
7. By default the API route will use `/parse` as a base. You can change this by setting the environment variable `PARSE_MOUNT`, for example in the CLI run run `export PARSE_MOUNT=/app` to set the path to `app`.
8. Your Parse Server is not running and is connected to your local database named `dev` in which the data is stored that you manage via Parse Server.

## Helpful Scripts
These scripts can help you to develop your app for Parse Server:

* `npm run watch` will start your Parse Server and restart if you make any changes.
* `npm run lint` will check the linting of your cloud code, tests and `index.js`, as defined in `.eslintrc.json`.
* `npm run lint-fix` will attempt fix the linting of your cloud code, tests and `index.js`.
* `npm run prettier` will help improve the formatting and layout of your cloud code, tests and `index.js`, as defined in `.prettierrc`.
* `npm run test` will run any tests that are written in `/spec`.
* `npm run coverage` will run tests and check coverage. Output is available in the `/coverage` folder.

# Using Parse Server

## Health Check

You can use the `/health` endpoint to verify that Parse Server is up and running. For example, for local deployment, enter this URL in your browser:

> [http://localhost:1337/parse/health](http://localhost:1337/parse/health)

If you deployed Parse Server remotely, change the URL accordingly.

## APIs and SDKs

Use the REST API, GraphQL API or any of the Parse SDKs to see Parse Server in action. Parse Server comes with a variety of SDKs to cover most common ecosystems and languages, such as JavaScript, Swift, ObjectiveC and Android just to name a few.

The following shows example requests when interacting with a local deployment of Parse Server. If you deployed Parse Server remotely, change the URL accordingly.

### REST API

Save object:
```sh
curl -X POST \
  -H "X-Parse-Application-Id: YOUR_APP_ID" \
  -H "Content-Type: application/json" \
  -d '{"score":1337}' \
  http://localhost:1337/parse/classes/GameScore
```

Call Cloud Code function:
```sh
curl -X POST \
  -H "X-Parse-Application-Id: YOUR_APP_ID" \
  -H "Content-Type: application/json" \
  -d "{}" \
  http://localhost:1337/parse/functions/hello
```

### JavaScript

```js
// Initialize SDK
Parse.initialize("YOUR_APP_ID", "unused");
Parse.serverURL = 'http://localhost:1337/parse';

// Save object
const obj = new Parse.Object('GameScore');
obj.set('score',1337);
await obj.save();

// Query object
const query = new Parse.Query('GameScore');
const objAgain = await query.get(obj.id);
```

### Android
```java
// Initialize SDK in the application class
Parse.initialize(new Parse.Configuration.Builder(getApplicationContext())
  .applicationId("YOUR_APP_ID")
  .server("http://localhost:1337/parse/")   // '/' important after 'parse'
  .build());

// Save object
ParseObject obj = new ParseObject("TestObject");
obj.put("foo", "bar");
obj.saveInBackground();
```

### iOS / tvOS / iPadOS / macOS (Swift)
```swift
// Initialize SDK in AppDelegate
Parse.initializeWithConfiguration(ParseClientConfiguration(block: {
  (configuration: ParseMutableClientConfiguration) -> Void in
    configuration.server = "http://localhost:1337/parse/" // '/' important after 'parse'
    configuration.applicationId = "YOUR_APP_ID"
}))
```
