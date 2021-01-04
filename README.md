# skip-postinstall

A simple, cross-platform way to skip a postinstall script by setting an environment variable

## How?

Yarn:

```shell
yarn add --dev skip-postinstall
```

NPM:

```shell
npm install --save-dev skip-postinstall
```

Add `skip-postinstall || ` to your postinstall script:

```json
{
    "scripts": {
        "postinstall": "skip-postinstall || node-gyp rebuild"
    }
}
```

When you want to skip your postinstall script, simply set the `SKIP_POSTINSTALL` environment variable and run your command:

```shell
SKIP_POSTINSTALL=1 yarn install
```

## Why?

Currently, there is no built-in way to only skip a top-level postinstall in Yarn or NPM. You can use the `--ignore-scripts` option, but that will ignore the postinstall scripts in all of your dependencies as well. You can also try this approach, but it doesn't work on Windows:

```json
{
    "scripts": {
        "postinstall": "test -n \"$SKIP_POSTINSTALL\" || node-gyp rebuild"
    }
}
```

`skip-postinstall` allows you to do this in a way that works on macOS, Linux, and Windows without any other dependencies (just [one line](https://github.com/rajivshah3/skip-postinstall/blob/main/index.js#L3) of code!)
