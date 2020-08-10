# dokku-deploy-from-registry

This plugin enables you to specify a registry for Dokku to pull an image from,
and then deploy it to an app.

The goal is to streamline the deployment process for container images.
For instance, in a CI job that builds an image and pushes it to a registry.


## Installation

```shell
dokku plugin:install https://github.com/yurihs/dokku-deploy-from-registry.git deploy-from-registry
```


## Usage

First, set the remote image repo for an app, like so:

```shell
dokku deploy-from-registry:set-remote-image-repo some-app registry.example.com/my-org/my-app
```

Then you can run

```shell
dokku deploy-from-registry some-app a1b2c3
```

to pull the `a1b2c3` tag and deploy it. After confirming that it works,
you can stick that command in your CI pipeline as a simple,
one-command deploy solution.

**Bonus:** use [dokku-acl](https://github.com/dokku-community/dokku-acl)
to restrict access to the deploy command.
Put `deploy-from-registry` in your `DOKKU_ACL_PER_APP_COMMANDS` environment variable,
and you should be good.


## Commands

```shell
deploy-from-registry <app> <tag>                          pull and deploy
deploy-from-registry:get-remote-image-repo <app>          get image repo
deploy-from-registry:set-remote-image-repo <app> <repo>   set image repo to pull from
deploy-from-registry:unset-remote-image-repo <app>        unset image repo
```

## License

[MIT License](https://github.com/yurihs/dokku-deploy-from-registry/blob/HEAD/LICENSE.txt)

The code is mostly glued together from the following projects. Their copyrights are listed in the license file.

- [Dokku core tags plugin](https://github.com/dokku/dokku/tree/HEAD/plugins/tags): scheduler tag creation trigger
- [dokku-registry plugin](https://github.com/dokku/dokku-registry): image pull handling, plugin config manager
