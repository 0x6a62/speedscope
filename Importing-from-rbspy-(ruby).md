[`rbspy`](https://rbspy.github.io/) is a ruby profiler that lets you profile Ruby processes that are already running.

`rbspy` has an explicit output format for speedscope (See [rbspy/rbspy#161](https://github.com/rbspy/rbspy/pull/161)).

To record a profile on an already-running process with `rbspy`, run:

```
sudo rbspy record --pid $PID --format speedscope --file profile.speedscope.json
```

Then drop the resulting `profile.speedscope.json` into https://www.speedscope.app/

To view it offline, you'll need to install speedscope via `npm`:

```
npm install -g speedscope
```

Then you should be able to open it like so:

```
speedscope /path/to/profile.json
```
