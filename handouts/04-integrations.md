# Git Integrations

There is a wide range of 3rd party tools, websites and services that can easily integrate with Git.

For this section, we will focus on using GitHub.

## Continuous Integration

- [MagnumCI](https://magnum-ci.com)
- [JenkinsCI](http://jenkins-ci.org/)
- [CircleCI](https://circleci.com/)
- [TravisCI](https://travis-ci.org/)
- [CodeShip](https://codeship.com/)

## Deployment
- [dploy](http://dploy.io/)

+ more

Trying to cover every possible tool is well outside the scope of this. However, we will go through an example of setting up Continious Integration with MagnumCI, and deployments with Heroku.


The project that I will use for this the 'git-training-app' that has been used as a demo during this session.

# Magnum CI

Magnum CI is a free CI server, and supports many source code providers such as Github, Bitbucket, Beanstalk, Gitlab and even self hosted.

Magnum CI is able to integrate with this by making use of the hooks that we covered in the previous section.

## Getting the project ready

To make things as smooth as possible, setting a 'test' script in your package.json is useful, otherwise we will need to configure MagnumCI manually to inform it of how to run the tests.

```json
"scripts": {
  "start": "node server/index.js",
  "test": "node node_modules/gulp/bin/gulp karma-ci"
}
```

Adding the project to Magnum CI:

* Dashboard -> Add a new Project
* Give it a name
* Provide the repository url
* Set the integration to Github
* Set the project type to Node JS

Once this is done, Mangum CI will prompt us for Github setup:

* Go to your GitHub repository
* Go to settings, and Webhooks & Services
* Add a Webhook, and paste the URL that MagnumCI provided.
* Select Deploy Keys, and Add Deploy Key
* Copy & Paste the key that Magnum CI provided
* Once done, back in Magnum CI - hit Test build, and go.

Now when a change is pushed to github, Magnum CI will try and run a build and run any tests.

# Heroku Deployment

Let's discuss using Git for deploying to Heroku.

# Git hooks

## What are Git hooks?

Built-in scripts Git executes before or after commits, pushes, and receives. These vary widely in functionality.


## How they work

Each Git repository comes with a `.git/hooks` folder where scripts for each hook that can be bound to.

To install a script, place any executable in the `.git/hooks` folder and name it according to the hook you mean to bind to.

## Client-side hooks

### `pre-commit`

Runs first, before the commit message prompt and allows you to inspect the snapshot that's about to be inspected.

Great for running tests, linting code and removing whitespaces.

### `prepare-commit-msg`

Runs before the commit message editor is launched but after the default message is created.

Great for editing the default message and templating.

### `commit-msg`

Runs after the commit message is saved.

Great for validating commit messages.

### `post-commit`

Runs after the entire commit is completed.

Great for notifications.

### `pre-rebase`

Runs before you rebase anything.

### `post-checkout`

Runs after a successful `git checkout`.

Great for setting up working environment, especially when large (untracked) binaries are involved.

### `post-merge`

Runs after a successful `git merge`.

## Server-side hooks

### `pre-receive`

Runs when handling a push from a client. Only

### `post-receive`

Runs after a push from a client is fully processed.

Great for notifying users and other systems such as the CI and IM applications.

### `update`

Very similar to the pre-receive hook but may run multiple times, depending on the amount of branches being pushed.

The `pre-receive` hook only runs once, no matter how many branches are pushed.

# Github Webhooks

## What is a Webhook?

Technical: An user defined HTTP callback that is triggered by a certain event that occurs at the source site.

Simple: A web service endpoint that listens to requests from a source and/or sends requests to a target.

Each hook can be configured to a specific service and any number of events.

## Setting up a Webhook

1. Go to the **Settings** page of your repository.
2. Click on **Webhooks & services**.
3. Click on **Add webhook**.

## Payload URL

This is the server endpoint that will handle the Webhook.

## Available events

commit\_comment | create | delete | deployment\_status | deployment | fork | gollum | issue\_comment | issues | member | page\_build | public | pull\_request\_review\_comment | pull\_request | push | release | status | team\_add watch

---

## Wildcard events

`*`

You'll receive every event.

## Payload

The POST request body, usually contains a JSON document.

Each event type has its own unique payload object.

## Sample Payload

```
POST /payload HTTP/1.1

Host: localhost:4567
X-Github-Delivery: 72d3162e-cc78-11e3-81ab-4c9367dc0958
User-Agent: GitHub Hookshot 044aadd
Content-Type: application/json
Content-Length: 6615
X-Github-Event: issue
```
```javascript
{
  "action": "opened",
  "issue": {
    "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
    "number": 1347,
    ...
    },
    "repository" : {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
        "login": "octocat",
        "id": 1,
        ...
        },
        ...
        },
        "sender": {
          "login": "octocat",
          "id": 1,
          ...
        }
      }
      ```
