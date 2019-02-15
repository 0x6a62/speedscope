[`stackprof`](https://github.com/tmm1/stackprof) is a sampling call-stack profiler for Ruby.

To record a profile, wrap your code in a `StackProf.run` block with `raw: true`, then save the JSON encoded version of the profile to a file. You'll need to be running `stackprof >= 0.2.11`.

```ruby
require 'json'
require 'stackprof'

profile = StackProf.run(mode: :wall, raw: true) do
  # Do your thing here
end

File.write('stackprof.json', JSON.generate(profile))
```

Then drop the resulting `stackprof.json` into https://www.speedscope.app/

To view it offline, you'll need to install speedscope via `npm`:

```
npm install -g speedscope
```

Then you should be able to open it like so:

```
speedscope stackprof.json
```
 