## Intro to Feathers: Deep dive in Hooks

Now we will continue our ongoing series about learning Feathers.js. Last time we learned about basic procedures, project structure and some details on Feathers Services. On this report, we'll try to understand more about Feathers Hooks.

[gif pudge]

## What are hooks
If you're coming from a Ruby on Rails background, or are familiar with Aspect Oriented Programming in Java, C#, C++ then you are already familiar with the concept of it. Hooks are pluggable middleware functions that can be registered *before*, *after*, *errors* of a Feathers Service method. We can choose to use one or chain multiple of them to fit our need. Using hooks aren't mandatory, meaning, you can just implement your desired functionality just by using Services. But, just like landing a successful hook by pudge brings your opponent carry in middle of your team, using Feathers Hooks will make your life a hell of a lot easier.


In RoR, we're familier with the *before* and *after* fileters. Let's think on how Viblo or Medium articles work when you're writing one. We don't want anyone else but us to see our post when it's still in draft stage. To achieve that, we'll use the *before_filter* call the *draft_or_private?* method and grant access to the appropriate person only.

```ruby
class Admin::ArticlesController < ApplicationController
  before_filter :deny_access, :unless => :draft_or_private?

  def show
    @article = Article.find(params[:id])
  end

  protected

    def draft_or_private?
        article = Article.find(params[:id])
        current_user.is_owner? ||  (article.draft? || article.private?) 
    end
end
```

This is in a nutshell, what Feathers Hooks are. We use before / after / error calls to chain offloaded methods, thus making our App more modular.

Example: We want to set a creation timestamp on our messages when they're created.
The code for that will be like this.
```js
const createdAt = async context => {
  context.data.createdAt = new Date();
  
  return context;
};

app.service('messages').hooks({
  before: {
    create: [ createdAt ]
  }
});

```

Feathers Hooks are:
Transport independent
Service agnostic (most of the time)

This pattern helps us keep our App DRY, flexible, composable and much easier to debug.

## Hook Flow
This is best explained in the [FeathersPlus](https://feathersjs.gitbooks.io/feathers-docs/guides/step-by-step/basic-feathers/all-about-hooks.html) book.


So, it's better if you read this part from there rather than reading my post. Because Viblo doesn't allow us to show `iframe` from another website, I'll post their explanation and examples here. But, all credit goes to the FeathersPlus book. 

### Method Hooks













## Learning Materials

[Feathers.js Guide#Hooks](https://docs.feathersjs.com/guides/basics/hooks.html#quick-example)

[Hooks API](https://docs.feathersjs.com/api/hooks.html#quick-example)

[Codepen example](https://codesandbox.io/s/feathers-hooks-common-test-9e0st)

[FeathersPlus - All about Hooks](https://feathersjs.gitbooks.io/feathers-docs/guides/step-by-step/basic-feathers/all-about-hooks.html)

[Design Pattern for Modern Web API](https://blog.feathersjs.com/design-patterns-for-modern-web-apis-1f046635215)

[AOP: Aspect Oriented Programming](https://en.wikipedia.org/wiki/Aspect-oriented_programming)

