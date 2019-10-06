[py-spy](https://github.com/benfred/py-spy) is a profiler that lets you profile Python processes that are already running.

py-spy has an explicit output format for speedscope (See https://github.com/benfred/py-spy/issues/115).

To record a profile on an already-running process with rbspy, run:

```
sudo py-spy record --pid $PID --format speedscope -o profile.speedscope.json
```
Then drop the resulting profile.speedscope.json into https://www.speedscope.app/

To view it offline, you'll need to install speedscope via npm:

```
npm install -g speedscope
```