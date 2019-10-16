.NET Core version 3 and higher supports creating trace profiles appropriate for Speedscope.  To do this install the trace tool.

```
dotnet tool install --global dotnet-trace
```

Once installed, a profile file can be created in two different ways.

1) Directly, define the format what collecting the trace results.

```
dotnet trace collect -p <process id> --format speedscope
```

2) If a trace has already been created in the NetTrace format, it can be converted.

```
dotnet trace convert --format speedscope <trace filename>
```

Once a properly formatted trace file exists, drop the resulting trace.speedscope.json into (https://www.speedscope.app/)

To view it offline, you'll need to install speedscope via npm:

```
npm install -g speedscope
```

Then you should be able to open it like so:

```
speedscope trace.speedscope.json
```

