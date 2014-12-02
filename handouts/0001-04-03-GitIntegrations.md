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

TODO: do this? - go as far as downloading/installing toolbelt, etc - or just show 'heroku create'?
