speedscope supports two profiler-agnostic formats which are designed for use by tools which generate custom profiles: speedscope's own file format, and Brendan Gregg's [collapsed stack format](https://github.com/BrendanGregg/flamegraph#2-fold-stacks).

## speedscope's file format

speedscope has a JSON-based file format. Its [JSON schema](http://json-schema.org/) can be found at https://www.speedscope.app/file-format-schema.json. 

The file format is documented here: [file-format-spec.ts](https://github.com/jlfwong/speedscope/blob/master/src/lib/file-format-spec.ts).

An example profile can be found here: [simple.speedscope.json](https://github.com/jlfwong/speedscope/blob/100578c536a3afab39fb6803d28913d12eac29c5/sample/profiles/speedscope/0.0.1/simple.speedscope.json).

If you author tools which generate this format, and speedscope should be able to import the result. This was e.g. the strategy used to add an output format for speedscope to `rbspy`. See [rbspy/rbspy#161](https://github.com/rbspy/rbspy/pull/161).

## Brendan Gregg's collapsed stack format
If you want a simpler file format to generate and don't care about the units used for each stack, then Brendan Gregg's collapsed stack format is easy to generate and understand.

The format consists of one stack trace per line, with the line ending with a single integer indicating the weight of that sample. Semicolons separate stack frames in the stack trace.

Here's an example profile in that format:

```
main;a;b;c 1
main;a;b;c 1
main;a;b;d 4
main;a;b;c 3
main;a;b 5
```

A more realistic example can be found here: [perf-vertex-stacks-01-collapsed-all.txt](https://github.com/jlfwong/speedscope/blob/100578c536a3afab39fb6803d28913d12eac29c5/sample/profiles/stackcollapse/perf-vertx-stacks-01-collapsed-all.txt)

## Google "Trace Event Format"

Used in `chrome://tracing`, the Google "Trace Event Format" is JSON-encoded, event-based format for logging performance events. See https://docs.google.com/document/d/1CvAClvFfyA5R-PhYUmn5OOQtYMH4h6I0nSsKchNAySU/preview#heading=h.xqopa5m0e28f for examples.

speedscope supports importing a subset of these events. Namely, it supports `B`, `E`, and `X` events, as well as the `M` events used to specify the names of processes and threads.