# feathers.js

# Creating a project

first you need the feathers-cli installed in your system.

```bash
npm install -g @feathersjs/cli
```

Now we need to generate the app we want to expirement with.

```bash
mkdir feathers-messages
cd feathers-messages
feathers generate app
```
You'll be shown a number of options you can choose from. For this example, we'll not be using any fully fledged database service, we'll use NeDB to store the data. Here are the options selected for the project.

[Pic1]
[pic2]


# Application architecture
[Pic3]
[Pic4]
The feathers.js official guide explains with great detail what each file and directory does. You can read more from [here](https://docs.feathersjs.com/guides/basics/generator.html#the-generated-files)


## Services
Services are at the core of a feathersjs projecct. We use services to interact with data like:

Reading or writing on the database

Calling another API

Working with 3rd party services (processing payment, sending mail, or getting data from any external api)

you can read more about services [here](https://docs.feathersjs.com/api/services.html)


To create a service we have this nifty generate command
```js
feathers generate service
```

again, it will ask you some details about the service.
lets name our service `messages`. Heres the options we choose.

[messages_service.pic]

now let's see what did the generator made for us.

```
git status

On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   src/services/index.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        src/models/messages.model.js
        src/services/messages/
        test/services/messages.test.js
```

so, it has modified the `services/index.js`
```js
const users = require('./users/users.service.js');
const messages = require('./messages/messages.service.js');
// eslint-disable-next-line no-unused-vars
module.exports = function (app) {
  app.configure(users);
  app.configure(messages);
};
```

and created a `messages.model.js`
```js
const NeDB = require('nedb');
const path = require('path');

module.exports = function (app) {
  const dbPath = app.get('nedb');
  const Model = new NeDB({
    filename: path.join(dbPath, 'messages.db'),
    autoload: true
  });

  return Model;
};
```

along with `messages.service.js`
```js
// Initializes the `messages` service on path `/messages`
const { Messages } = require('./messages.class');
const createModel = require('../../models/messages.model');
const hooks = require('./messages.hooks');

module.exports = function (app) {
  const Model = createModel(app);
  const paginate = app.get('paginate');

  const options = {
    Model,
    paginate
  };

  // Initialize our service with any options it requires
  app.use('/messages', new Messages(options, app));

  // Get our initialized service so that we can register hooks
  const service = app.service('messages');

  service.hooks(hooks);
};
```


## Hooks


## Resources

[Feathers.js official docs](https://docs.feathersjs.com/guides/basics/starting.html)
