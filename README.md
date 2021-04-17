# Getcho Backend

- GraphQL
- ES6, Babel
- Mongo / Mongoose

## Documentation

Global Getcho project documentation can be found in the frontend repo [here](https://github.com/koptional-org/sendit_mobile). This README will only document items specific to the backend.

## env

```bash
cp env-example .env
# now update the items in .env to match real credentials
```

## Scripts

To create objectId lookup fields for quotes and orders (**MAKE SURE THAT YOU ARE USING THE APPROPRIATE DB IN YOUR .env FILE**):

```bash
npx babel-node src/scripts/createOrderUserLookup.js
```

## Testing

The Getcho test suite contains a few different types of tests:

- `models`
- `ee`

### Model Tests

For the rare, complex [Mongoose](https://mongoosejs.com/) model, we will try to test methods, statics, and persistence.

Currently there is only one model test, and it is for testing the intricacies of the User model. Most models exist purely as a means for data persistence. However, the `User` leverages [Mongoose methods](https://mongoosejs.com/docs/2.7.x/docs/methods-statics.html) for hashing passwords and validating passwords.

### EE Tests

On the testing pyramid, end-to-end tests are the most cumbersome but also the most holistic. Getcho Backend's test footprint is relatively small, hence the majority of tests are ee.

End-to-end tests for the Getcho backend require that you run a test server in one process using the following command

```bash
npm run test:run-server
```

You then can execute a specific test- **found in the `/test/` directory with a `spec.js` extension** like so:

```bash
# Can replace wiht any file, or use test/**/*.spec.js to run all files
npm run test:grep -- test/ee/quotes.spec.js
```

Please make sure that you have a local Mongo daemon running for this to work!

## TODO

- [ ] git ignore dist, have deployment build this file automatically
- [ ] Fully migrate from duhardg@gtcho.com to developer@koptional for postmates integration
- [ ] Set up testing. See [here](https://www.apollographql.com/docs/apollo-server/testing/testing/). Need to run express server and hit queries somehow

## Vendors

- MongoAtlas for Mongodb Connection
  - developer@koptional.com is the account
  - For production, cluster0 database = test
  - For development, cluster0 database = development
- Postmates
  - Production Developer Account Login: duhartdg@gtcho.com
  - Local Development Account Login: jackconsidine3@gmail.com
  - Remote developer account login: developer@koptional.com

### POSTMATES WEBHOOKS

- Can set production and sandbox webhooks on each postmates account
- currently the production webhook points to the prod API endpoint, though most app installations point to the staging URL, so it's crucial for our deployment pipeline that we remember to "promote staging to production"
