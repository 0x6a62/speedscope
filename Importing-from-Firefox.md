To record a performance profile in Firefox, open the developer tools and switch to the performance tab.

Click the "Start Recording Performance" button.

!["Start Recording Performance" button in Firefox](https://i.imgur.com/KA6PnBc.png)

When you're done recording, click the "Stop Recording Performance" button.

!["Stop Recording Performance" button in Firefox](https://i.imgur.com/JoQfXsm.png)

When it's finished processing, click on "save".

!["save" link in Firefox](https://i.imgur.com/UO0u7iE.png)

This should save as a filename like `profile.json`.

You should be able to open that file in https://www.speedscope.app/.

To view it offline, you'll need to install speedscope via `npm`:

```
npm install -g speedscope
```

Then you should be able to open it like so:

```
speedscope /path/to/profile.json
```