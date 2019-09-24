# feathers.js

# How it's structured

## Services

## Hooks

## Creating a project

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

## Application architecture
[Pic3]
[Pic4]
The feathers.js official guide explains with great detail what each file and directory does. You can read more from [here](https://docs.feathersjs.com/guides/basics/generator.html#the-generated-files)
