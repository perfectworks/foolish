# A foolish front-end building script

Building is not fun, especially when we have so many 3rd-party tools to make a building system for you (or your team).

After 8 years front-end development (from 2008), I decide to jump out of this shit pit. So, here it is.

## Concept

* Simpler is better.
* Convention over configuration. (Actully, there is nothing you can change)

## Should I use this?

This build script is for single page app. It will concat all scripts to one and auto reversion all assets referenced by html and css. There is no framework specified.

## Installation

`npm install -g foolish`

## How to use

* Building project: `foolish`
* Start a dev server: `foolish server`

## Document

### Filename conventions

Any directory is a valid foolish project, even if it's empty. Some filename is special but not required:

1. `index.html`: this is the landing page.
2. `main.js`: this script will be at the top in combiled script.
3. `run.js`: this script will be at the ned in combiled script.
4. `main.less`: write your less style here.
5. `app.js`: only use this in `index.html`, your project should *not* have this file, it's combined output script filename.
5. `app.css`: only use this in `index.html`, your project should *not* have this file, it's compile style filename.

Here is a basic web page project which contains script and stylesheet:

1. `mkdir my-foolish-project && cd my-follish-project`.
2. `echo '<link href="app.css" rel="stylesheet"></link>' > index.html`.
3. `echo '<script src="app.js" type="text/javascript"></script>' >> index.html`.
4. `touch main.js`.
5. `touch main.less`.

### Development Server

Use command `foolish server`, a small http server will start listening on port 3000.

Look at the initialize step, I think you already realized there is no `app.js` or `app.css`. Those files are virtual, which generated by development server or building script.

`app.js` will load all your scripts, `app.css` is generated from `main.less`.

You can use `--port` parameter to change the server port.

### Building

Just run `foolish` under your project directory, then you will get a `dist` directory which contains what you want.

The building prosess is simple:

1. Concat all `.js` files in your project directory (except `node_modules`) to `dist/app.js`. `main.js` will at head and `run.js` will be the last.
2. Compile `main.less` to `dist/app.css`.
3. Find assets which refrenced by `index.html` and `dist/app.css`, copy them to `dist` directory.
4. Reversion them all.
5. If there is a `--prefix` parameter, all resource will add it.

## FAQ

### Q: How can I import 3rd-party modules?
A: Just create a `<script>` tag in `index.html` to reference a script file. The file location can be in internect (like CDN server) or just a local dependency in `node_modules` (`npm install` is welcome).

### Q: Can I add some pre-process plugin like coffee or babel?
A: Sure but not in `foolish`. You can do this by shell command. 

## Contribution

PR is welcome. I'll very happy if someone tell me some feature is useless and can be drop out.

## License

MIT

[a boring frontend-end developer]:http://thebfed.com

