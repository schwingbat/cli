# CLI

A reasonably straightforward CLI library for creating utilities with multiple commands.

## Usage

```javascript
#!/usr/bin/env node

const CLI = require("@schwingbat/cli");

const { command, run } = CLI({
  name: "util",
  version: "1.0.0"
});

command({
  signature: "greet <name>",
  description: "print a greeting",
  examples: ["util greet Bob"],
  arguments: [
    {
      name: "name",
      description: "a name to use for the greeting",
      default: "World"
    }
  ],
  options: [
    {
      name: "caps",
      short: "c"
      description: "scream the greeting",
      type: parseDateTime
    }
  ],
  run: async function(args) {
    let message = `Hello, ${args.name}!`;

    if (args.options.caps) {
      message = message.toUpperCase();
    }

    console.log(message);
  }
});

// Run with CLI arguments.
run( process.argv.slice(2) );
```

Add this script to your `package.json` `bin` object:

```json
{
  "bin": {
    "util": "./util.js"
  }
}
```

Now do an `npm install -g .` on your package and you can now call it like so:

```bash
$ util greet
Hello, World!

$ util greet Bob
Hello, Bob!

$ util greet Bob --caps
HELLO, BOB!

$ util greet human -c
HELLO, HUMAN!
```