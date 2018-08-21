There are two ways to import profiles from Node.js: using the Chrome inspector, and using `node --prof`.

## Importing from the Chrome inspector

Node now has built-in support to be inspected using Chrome. [This article by Paul Irish](https://medium.com/@paul_irish/debugging-node-js-nightlies-with-chrome-devtools-7c4a1b95ae27) has more details.

Run your program with `--inspect`. For example, this is how you'd profile a build of [parcel](https://parceljs.org/)

```
node --inspect node_modules/.bin/parcel assets/index.html
```

Now visit `chrome://inspect`, and you should see something like this:

![chrome://inspect page](https://i.imgur.com/eziWDTO.png)

Click the "inspect" link. This should open a developer tools window.

![Clicking the start button](https://i.imgur.com/vTGZEgy.png)

Click the start button to start recording a profile.

![Clicking the stop button](https://i.imgur.com/WrMbOld.png)

Now force the node behavior you're trying to profile (e.g. by loading the webpage it serves). When you're done, click the stop button.

![Clicking on "save"](https://i.imgur.com/lcxc3tZ.png)

Click on "save" to save the recorded profile. Save it with the default `.cpuprofile` file extension.

![Saving the ".cpuprofile" file](https://i.imgur.com/pMG0RQ0.png)


You should be able to open that file in https://www.speedscope.app/.

To view it offline, you'll need to install speedscope via `npm`:

```
npm install -g speedscope
```

Then you should be able to open it like so:

```
speedscope /path/to/profile.json
```

## Importing from `node --prof`

If you record profiling information like so:

```
node --prof /path/to/my/script.js
```

Then this will generate one or more `isolate*.log` files. You can
convert these files into a file that can be imported into speedscope
like so:

```
node --prof-process --preprocess -j isolate*.log > profile.v8log.json
```

You should be able to open that file in https://www.speedscope.app/.

To view it offline, you'll need to install speedscope via `npm`:

```
npm install -g speedscope
```

Then you should be able to open it like so:

```
speedscope /path/to/profile.v8log.json
```

You can also pipe the output of `node --prof-process` directly to speedscope with a trailing `-` like so:

```
node --prof-process --preprocess -j isolate*.log | speedscope -
```