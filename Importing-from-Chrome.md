To record a performance profile in Chrome, open the developer tools and switch to the performance tab.

Click the record button.

![Click record button in Chrome](https://i.imgur.com/wTKhKOD.png)

When you're done recording, click the "Stop" button.

![Click stop button in Chrome](https://i.imgur.com/Mlddiac.png)

When it's finished processing, click the "Save profile" button.

![Click the Save profile button](https://i.imgur.com/8KVUPWl.png)

This should save as a filename like `Profile-20180820T095940.json`.

You should be able to open that file in https://www.speedscope.app/.

To view it offline, you'll need to install speedscope via `npm`:

```
npm install -g speedscope
```

Then you should be able to open it like so:

```
speedscope /path/to/profile.json
```