# mono-repo-bootstrap

> A starting point for distributed monolith-type projects that don't want to be mono-repo projects

If you have a bunch of separate git repositories containing modules that need to be released in concert or that are riddled with cross-dependencies, this ~~is~~ could be the project setup for you.

```console
$ git clone https://github.com/achingbrain/mono-repo-bootstrap.git
$ mv mono-repo-bootstrap my-project-name
$ cd my-project-name
$ rm -rf .git # this is your project now
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
$ npm run reset && npm i
```

## Publishing modules

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

## Gotchas

 * This setup hoists dependencies to the root. Sometimes you can end up with modules using a dep that isn't in their `package.json`, which works until you publish it and everything explodes at runtime.  You have three options:
    1. [Turn off hoisting](https://github.com/achingbrain/mono-repo-bootstrap/blob/master/lerna.json#L9) (slows everything down, not recommended)
    1. Use [`dependency-check`](https://www.npmjs.com/package/dependency-check) in a linting step.
    1. Configure your ci to test your modules independently
