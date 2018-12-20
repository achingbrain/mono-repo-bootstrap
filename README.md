# mono-repo-bootstrap

> A starting point for a mono-repo projects

```console
$ git clone https://github.com/achingbrain/mono-repo-bootstrap.git
$ mv mono-repo-bootstrap my-project-name
$ cd my-project-name
$ rm -rf .git # this is your project now
$ mkdir packages # your packages will go here
$ cd packages
$ git clone ... # clone your various repos
$ cd ../
$ npm i # will bootstrap and cross-link all packages
```

No need to install lerna globally.

## Adding new dependencies to your modules

If you add a dependency to a package, you need to re-bootstrap and crosslink:

```console
$ # in the mono-repo root
$ npm run reset
```

## Publshing modules

```console
$ # in the mono-repo root
$ npm run publish
```

Publishing using `npm run publish` with a OTP enabled account needs a [workaround](https://github.com/lerna/lerna/issues/1091).

Spoiler (nb. all your modules must finish publishing before the OTP expires..):

```console
$ # in the mono-repo root
$ NPM_CONFIG_OTP=123456 npm run publish
```
