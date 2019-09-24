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

## Hooks


## Resources

[Feathers.js official docs](https://docs.feathersjs.com/guides/basics/starting.html)
