# Travis CI example [![Build Status](https://travis-ci.org/surge-sh/example-travis.svg?branch=master)](https://travis-ci.org/surge-sh/example-travis)

An example using [Travis CI](https://travis-ci.org) for continuous deployment to [Surge.sh](https://surge.sh).

## Getting started

Continuous Integration services like [Travis CI](https://travis-ci.org/) make it possible to run Surge and publish your project each time you push to a GitHub repository. This also makes it possible to publish each time your tests pass, or when someone opens up a pull request.

1. Get your token
2. Add your project’s repository to Travis CI
3. Push a `.travis.yml` file that will run the `surge` command

### Get your token

Your secret Surge token allows services like Travis CI to login and publish projects on your behalf. Get your Surge token by running the following command in your terminal:

```
surge token
```

You’ll be asked to login again, and afterwards your token will be displayed like this:

```
token: a142e09a6b13a21be512b141241c7123
```

![](https://surge.sh/images/help/integrating-with-travis-ci.gif)

### Add your project’s repository to Travis CI

Now you are ready to login and setup your project on Travis CI. Add your project’s GitHub repo to your list of Travis CI projects. The screenshots are using the [surge-sh/example-travis](https://github.com/surge-sh/example-travis) repo:

![](https://surge.sh/images/help/integrating-with-travis-ci-2.png)

Press _Environment Variables_ next, and you’ll be able to secretly add your email address and token so Travis CI can login to Surge for you:

![](https://surge.sh/images/help/integrating-with-travis-ci-3.png)

Create one environment variable called:

```
SURGE_LOGIN
```

…and set it to the email address you use with Surge. Next, add another environment variable called:

```
SURGE_TOKEN
```

…and set it to your Surge token.

### Push a `.travis.yml` file that will run the `surge` command

Travis CI machines won’t have Surge installed by default, so you also need to save Surge as a [development dependency] to your project. You can do this by creating a `package.json` file if you don’t have one already. Run the following command in your terminal to be walked through making this file (you can hit enter to accept the defaults):

```sh
npm init
```

You will end up with a file that looks [something like this one](https://github.com/surge-sh/example-travisci/blob/master/package.json).

Next, run this command to save Surge as a `devDependency`, so Travis CI will install it:

```sh
npm install --save-dev surge
```

The last step is to add a `.travis.yml` file to your project. Travis CI uses this

> file in the root of your repository to learn about your project and how you want your builds to be executed. `.travis.yml` can be very minimalistic or have a lot of customization in it.
> <footer>Travis CI <cite>[.travis.yml file: what it is and how it is used](http://docs.travis-ci.com/user/build-configuration/#.travis.yml-file%3A-what-it-is-and-how-it-is-used)</cite></footer>

Your `.travis.yml` file should loook like this:

```yml
language: node_js
node_js:
  - "0.12"
after_success:
  - surge --project ./path/to/your-project --domain your-project.surge.sh
```

After you push you successfully push to your repository, Travis CI will run `surge`. Replace `./path/to/your-project` with the path to the source files in your repository, and `your-project.surge.sh` with the domain you’d like to publish to.

There are more examples of what you can do with a `.travis.yml` file [directly from Travis CI](http://docs.travis-ci.com/user/languages/javascript-with-nodejs/).

## License

[The MIT License (MIT)](LICENSE.md)

Copyright © 2015 [Chloi Inc.](http://chloi.io)
