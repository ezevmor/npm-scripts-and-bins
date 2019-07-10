# Npm scripts and bins

This is a quick look to the script and bind creation in a package.json.

## Scripts

We can consider two types of scripts:
### 1. Hooks
They are executed automatically when any default npm task (`npm install` or `npm start`, etc) is executed.

So we can configure:
```
{
    "scripts": {
        "install": "npm install -D yarn webpack"
    }
}
```

Although isn't useful this example allows us try something simple; this script will install yarn and webpack in devDependencies after been installed all project dependencies

You can take a look of all available hook scripts here: [npm-scripts](https://docs.npmjs.com/misc/scripts)

### 2. Custom
They must be executed manually.

So we can configure:
```
{
    "scripts": {
        "uninstall-dev-tools": "npm uninstall yarn webpack"
    }
}
```
and execute with:
```
npm run uninstall-dev-tools
```

## Bins
They allows us to link scripts to the nodejs command line.
To start we need to create a script file:

world-greeting.js
```
#!/usr/bin/env node
const [,, ...args] = process.argv;

console.log(`hello world ${args}`);
```

The first line `#!/usr/bin/env node` defines that interpreter of the file should be `/usr/bin/env node`.
The second line stores all the arguments given in the command line and the third one prints a message with them.

Then we have to config the bin into the package.json mapping our script file:

```
{
    "bin": {
        "greet-world": "bins/world-greeting.js",
    }
}
```

finally we link the bin:
```
npm link
```

Now we can execute the `greet-world` command directly from the console:
```
greet-world 
    => prints "hello world"

greet-world friend
    => prints "hello world friend"
```

## References
* [Tu, yo y package.json](https://medium.com/noders/t%C3%BA-yo-y-package-json-9553929fb2e3)
* [Nodejs command-line package](https://medium.com/netscape/a-guide-to-create-a-nodejs-command-line-package-c2166ad0452e)

