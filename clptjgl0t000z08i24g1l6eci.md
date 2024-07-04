---
title: "Installing Bun."
datePublished: Wed Dec 06 2023 09:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clptjgl0t000z08i24g1l6eci
slug: installing-bun
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705131887183/bbe84be0-6e2c-4262-ad83-2c025bf97e3a.png
tags: jest, bundler, package-manager, bun, javascript-runtime

---

## TL;DR.

Bun is a fast JavaScript runtime with TypeScript support. It is designed to be a drop-in replacement for Node.js. The Bun CLI has features like a runtime, bundler, test runner, package runner, package manager, and APIs. This post:

* Covers Bun's installation,
    
* Includes a quick start guide,
    
* Introduces the package manager,
    
* Describes TypeScript integration for it's APIs, and
    
* Suggests how templates can be built, and used, for custom initialisations.
    

> ***Attribution:***
> 
> [https://bun.sh/docs](https://bun.sh/docs)

## An Introduction.

Bun is fast because it is written in a low-level programming language called Zig. Unlike other runtimes that use Chrome V8, Bun is powered by JavaScriptCore, the same JavaScript engine that is used by Apple Safari.

> The purpose of this post is to introduce the Bun JS runtime.

Bun 1.0 was released on Friday 8th September 2023 and the CLI includes:

* TypeScript support,
    
* A runtime (bun run),
    
* A bundler (bun build),
    
* A test runner (bun test),
    
* A package runner (bunx),
    
* A package manager (bun install), and
    
* A small (but growing) collection of useful APIs.
    

I will touch on each of these topics as per [the official documentation](https://bun.sh/docs).

## The Big Picture.

A JavaScript runtime allows JS code to run on the server. The main advantage lies in the reduction of context switching: JavaScript running on the server *and* in the browser means there is ONE programming language involved during development. At least, that was an intent when Node was launched in 2009.

The introduction of ECMAScript 2015, colloquially called ES6, introduced new JavaScript features like const, let, arrow functions, and other features. Further developments would threaten jQuery, although it is still a very popular library.

Each year, ECMA would issue updated JavaScript standards and each browser vendor would release new features to match. As JavaScript continued to evolve, modern development practices also changed. These transitions were due to new tools and practices that evolved, hand in hand, with the annual ECMA releases.

The current range of development tools is wide and varied. Also, it is common to see a new framework, language, library, or runtime *launch each week*. For instance, Bun 1.0 and the Mojo Local Installer were unveiled *on the same day*!!

Suffice it to say that software engineering is a continually evolving field.

## Prerequisites.

* A Linux-based distro (I use Ubuntu),
    
* A remote 'bun' container on my homelab [as per these instructions](https://solodev.app/1-of-3-setting-up-a-remote-container).
    
* A remote connection from my workstation [as per these instructions](https://solodev.app/2-of-3-setting-up-a-remote-connection).
    
* A hardened 'bun' container on my homelab [as per these instructions](https://solodev.app/3-of-3-hardening-the-remote-container).
    

> NOTE: The purpose of using containers is to isolate any running processes from other containers and the host system.

## Installing Bun.

* I connect VS Code to the 'bun' container (which requires the Microsoft '*Remote - SSH*' extension and the '*F1 -&gt; Remote-SSH: Open SSH Host...*' command.)
    
* From the VS Code terminal (use `CTRL + ~` to show/hide the terminal) I install the unzip package:
    

```javascript
sudo apt install unzip -y
```

* I install Bun:
    

```javascript
curl -fsSL https://bun.sh/install | bash
```

* I set the source:
    

```javascript
source $HOME/.bashrc
```

* I check the version:
    

```javascript
bun -v
```

## Upgrading and Uninstalling Bun.

* I can, if needed, upgrade Bun:
    

```javascript
bun upgrade
```

* I can, if needed, uninstall Bun:
    

```javascript
rm -rf ~/.bun
```

## Quickstart1.

* I make a 'quickstart1' directory:
    

```javascript
mkdir quickstart1
```

* I change to that directory:
    

```javascript
cd quickstart1
```

* I scaffold a new project (and accept all the defaults):
    

```javascript
bun init -y
```

## Hello, Bun as a Hot Reload File.

* I add the following to 'index.ts' file and save the changes:
    

```javascript
const server = Bun.serve({
  port: 3000,
  fetch(req) {
    return new Response("Hello, from Bun.");
  },
});

console.log(`Listening on http://localhost:${server.port} ...`);
```

* I run the 'index.ts' file from the terminal:
    

```javascript
bun --hot run index.ts
```

* I open a browser on my workstation and point it to 192.168.188.52:3000.
    
* I stop the server (CTRL + C).
    

## Hello, Bun as a Hot Reload Script.

* I open the 'package.json' file.
    
* I add the following:
    

```javascript
  "scripts": {
    "start": "bun --hot run index.ts"
  },
```

* I run the script from the terminal:
    

```javascript
bun run start
```

* I open a browser on my workstation and point it to 192.168.188.52:3000.
    
* I stop the server (CTRL + C).
    

## Installing a Package.

* I install the 'figlet' package:
    

```javascript
bun add figlet
```

* FOR TYPESCRIPT USERS ONLY:
    

```javascript
bun add -d @types/figlet
```

* I replace the contents of the 'index.ts' file:
    

```javascript
import figlet from "figlet";

const server = Bun.serve({
  fetch() {
    const body = figlet.textSync("Hello, from Figlet Bun!");
    return new Response(body);
  },
  port: 3000,
});
```

* I use the 'package.json' script command to run the server.
    

```javascript
bun run start
```

* I open a browser on my workstation and point it to 192.168.188.52:3000.
    
* I stop the server (CTRL + C).
    

## TypeScript.

* I install the TypeScript definitions for the built-in APIs:
    

```javascript
bun add -d bun-types
```

* I add the following to my 'tsconfig.json' file:
    

```javascript
{
  "compilerOptions": {
    "types": ["bun-types"],
  }
}
```

> NOTE: I can now reference the `Bun` global in my TypeScript files.

* I add the following to the bottom of the 'index.ts' file:
    

```javascript
console.log(`Bun version: ` + Bun.version);
```

* The following 'tsconfig.json' entries are a set of recommended `compilerOptions` for a Bun project:
    

```javascript
{
  "compilerOptions": {
    // add Bun type definitions
    "types": ["bun-types"],

    // enable latest features
    "lib": ["esnext"],
    "module": "esnext",
    "target": "esnext",

    // if TS 5.x+
    "moduleResolution": "bundler",
    "noEmit": true,
    "allowImportingTsExtensions": true,
    "moduleDetection": "force",
    // if TS 4.x or earlier
    // "moduleResolution": "nodenext",

    "jsx": "react-jsx", // support JSX
    "allowJs": true, // allow importing `.js` from `.ts`
    "esModuleInterop": true, // allow default imports for CommonJS modules

    // best practices
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true
  }
}
```

> NOTE: If I run `bun init` in a new directory, this `tsconfig.json` will be generated automatically.

* I use the 'package.json' script command to run the server.
    

```javascript
bun run start
```

* I open a browser on my workstation and point it to 192.168.188.52:3000.
    
* I stop the server (CTRL + C).
    

## DOM Types.

* If I need to add DOM types to my project, I add the following [triple-slash directives](https://www.typescriptlang.org/docs/handbook/triple-slash-directives.html) at the top of any TypeScript file in my project:
    

```javascript
/// <reference lib="dom" />
/// <reference lib="dom.iterable" />
```

## Templates.

* In VS Code, I close the 'quickstart1' directory using File &gt; Close Folder \[CTRL + K F\].
    
* In the VS Code terminal, I make a 'quickstart2' directory in the home (~) directory:
    

```javascript
mkdir quickstart2
```

* In VS Code, I click the blue 'Open Folder' button, select the 'quickstart2' directory, and click the blue 'OK' button.
    
* I open the VS Code terminal with CTRL + ~.
    
* In the terminal, I change to the 'quickstart2' directory:
    

```javascript
cd quickstart2
```

* I scaffold an empty project with the interactive `bun init` command (and I use the -y flag to auto-accept the default settings):
    

```javascript
bun init -y
```

* I template a new Bun project with `bun create`:
    

```javascript
bun create <template> [<destination>]
```

## From a GitHub Template.

* I can download the contents of a GitHub repo to disk:
    

```javascript
bun create <user>/<repo>
```

* I can also use the following command:
    

```javascript
bun create github.com/<user>/<repo>
```

* I can optionally specify a name for the destination folder (otherwise the repo name will be used):
    

```javascript
bun create <user>/<repo> mydir
```

* I can also use the following command:
    

```javascript
bun create github.com/<user>/<repo> mydir
```

## From a Local Template.

* My templates should live in one of the following directories:
    
    * `$HOME/.bun-create/<name>` (for global templates), and
        
    * `<project root>/.bun-create/<name>` (for project-specific templates).
        

> NOTE: I can customize the global template path by setting the `BUN_CREATE_DIR` environment variable.

* I navigate to `$HOME/.bun-create`:
    

```bash
cd $HOME/.bun-create
```

* I create a new directory with the desired name of my template:
    

```bash
mkdir foo
```

* I change to the new directory:
    

```bash
cd foo
```

* I create a `package.json` file:
    

```bash
touch ./package.json
```

* I open the file with Nano:
    

```bash
sudo nano package.json
```

* I add the following, save the changes, and exit Nano:
    

```json
{
  "name": "foo"
}
```

* I create a new directory:
    

```bash
mkdir ~/quickstart3
```

* I change to that directory:
    

```bash
cd ~/quickstart3
```

* I verify that Bun is correctly finding my local template:
    

```javascript
bun create foo
```

## **Setup Logic for Templates.**

I can specify pre- and post-install setup scripts in the `"bun-create"` section of my local template's `package.json` file:

```json
{
  "name": "@bun-examples/simplereact",
  "version": "0.0.1",
  "main": "index.js",
  "dependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  },
  "bun-create": {
    "preinstall": "echo 'Installing...'", // a single command
    "postinstall": ["echo 'Done!'"], // an array of commands
    "start": "bun run echo 'Hello world!'"
  }
}
```

> NOTE: After cloning a template, `bun create` will automatically remove the `"bun-create"` section from `package.json` before writing it to the destination folder.

## CLI Flags.

| **Flag** | **Description** |
| --- | --- |
| `--force` | Overwrite existing files |
| `--no-install` | Skip installing `node_modules` & tasks |
| `--no-git` | Don’t initialize a git repository |
| `--open` | Start & open in-browser after finish |

## Environment Variables.

| **Name** | **Description** |
| --- | --- |
| `GITHUB_API_DOMAIN` | If you’re using a GitHub enterprise or a proxy, you can customize the GitHub domain Bun pings for downloads |
| `GITHUB_API_TOKEN` | This lets `bun create` work with private repositories or if you get rate-limited |

## How `bun create` Works.

When you run `bun create ${template} ${destination}`, here’s what happens:

IF remote template

1. GET [`registry.npmjs.org/@bun-examples/${template}/latest`](http://registry.npmjs.org/@bun-examples/$%7Btemplate%7D/latest) and parse it
    
2. GET [`registry.npmjs.org/@bun-examples/${template}/-/${template}-${latestVersion}.tgz`](http://registry.npmjs.org/@bun-examples/$%7Btemplate%7D/-/$%7Btemplate%7D-$%7BlatestVersion%7D.tgz)
    
3. Decompress & extract `${template}-${latestVersion}.tgz` into `${destination}`
    
    * If there are files that would overwrite, warn and exit unless `--force` is passed
        

IF GitHub repo

1. Download the tarball from GitHub’s API
    
2. Decompress & extract into `${destination}`
    
    * If there are files that would overwrite, warn and exit unless `--force` is passed
        

ELSE IF local template

1. Open local template folder
    
2. Delete destination directory recursively
    
3. Copy files recursively using the fastest system calls available (on macOS `fcopyfile` and Linux, `copy_file_range`). Do not copy or traverse into `node_modules` folder if exists (this alone makes it faster than `cp`)
    
4. Parse the `package.json` (again!), update `name` to be `${basename(destination)}`, remove the `bun-create` section from the `package.json` and save the updated `package.json` to disk.
    
    * IF Next.js is detected, add `bun-framework-next` to the list of dependencies
        
    * IF Create React App is detected, add the entry point in /src/index.{js,jsx,ts,tsx} to `public/index.html`
        
    * IF Relay is detected, add `bun-macro-relay` so that Relay works
        
5. Auto-detect the npm client, preferring `pnpm`, `yarn` (v1), and lastly `npm`
    
6. Run any tasks defined in `"bun-create": { "preinstall" }` with the npm client
    
7. Run `${npmClient} install` unless `--no-install` is passed OR no dependencies are in package.json
    
8. Run any tasks defined in `"bun-create": { "preinstall" }` with the npm client
    
9. Run `git init; git add -A .; git commit -am "Initial Commit";`
    
    * Rename `gitignore` to `.gitignore`. NPM automatically removes `.gitignore` files from appearing in packages.
        
    * If there are dependencies, this runs in a separate thread concurrently while node\_modules are being installed
        
    * Using libgit2 if available was tested and performed 3x slower in microbenchmarks
        

## Ecosystem.

The following is a collection of guides for using various tools and frameworks with Bun.

### App Development.

| Ecosystem for Bun | Native Support and Site |
| --- | --- |
| [Nuxt](https://bun.sh/guides/ecosystem/nuxt) | Yes |
| [Prisma](https://bun.sh/guides/ecosystem/prisma) | Yes |
| [React and JSX](https://bun.sh/guides/ecosystem/react) | Yes |
| [SveltKit](https://bun.sh/guides/ecosystem/sveltekit) | Yes (similar to Next and Nuxt) |
| [A Discord bot](https://bun.sh/guides/ecosystem/discordjs) | [Yes](https://kit.svelte.dev/) |
| [Astro](https://bun.sh/guides/ecosystem/astro) | No |
| [Next.js](https://bun.sh/guides/ecosystem/nextjs) | No |
| [Remix](https://bun.sh/guides/ecosystem/remix) | No |
| [SolidStart](https://bun.sh/guides/ecosystem/solidstart) | No |
| [Vite](https://bun.sh/guides/ecosystem/vite) | No |

### Server Development.

| Ecosystem | Description |
| --- | --- |
| [Hono](https://bun.sh/guides/ecosystem/hono) | [Hono](https://github.com/honojs/hono) is a lightweight ultrafast web framework designed for the edge. |
| [Elysia](https://bun.sh/guides/ecosystem/elysia) | [Elysia](https://elysiajs.com/) is a Bun-first performance-focused web framework. |
| [Express](https://bun.sh/guides/ecosystem/express) | [Express](https://expressjs.com/) provides a thin layer of fundamental web application features. |
| [StricJS](https://bun.sh/guides/ecosystem/stric) | [StricJS](https://stricjs.netlify.app/#/) is a Bun framework for building high-performance web applications and APIs. |
| [MongoDB and Mongoose](https://bun.sh/guides/ecosystem/mongoose) | MongoDB and Mongoose work out of the box with Bun. |
| [SSR for React](https://bun.sh/guides/ecosystem/ssr-react) | Server-Side Rendering (unlike Static Site Generation, Client-Side Rendering, and Incremental Site Rendering). |

## The Results.

Bun offers a powerful and efficient alternative to Node.js, providing a range of features such as TypeScript support, a bundler, test runner, package runner, and package manager. By following the installation and quickstart guide, I can easily adopt Bun and harness its potential to improve my JavaScript projects.

## In Conclusion.

Although Bun has finally released version 1.0, it has a long way to go if it wants to match the features provided by Node. Initial support for Bun appears very high but as more developers evaluate its features, shortcomings are bound to appear. The real test involves how quickly the developers can address these failings.

Until next time: Be safe, be kind, be awesome.