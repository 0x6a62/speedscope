[`pprof`](https://golang.org/pkg/runtime/pprof/) is a tool for capturing profiling data for the Go programming language. The two most common ways of profiling go programs are by writing a `.prof` file to disk, and by downloading profiling information from a running server instrumented with `net/http/pprof`.

# Importing from a `.prof` file written to disk

You can write CPU profiles to disk in a program via the `pprof.StartCPUProfile` and `pprof.StopCPUProfile` commands.

Let's say you have a program like this in `simple.go`.

```go
// simple.go
package main

import "flag"
import "runtime/pprof"
import "os"

var cpuprofile = flag.String("cpuprofile", "", "write cpu profile to file")

func main() {
	flag.Parse()
	if *cpuprofile != "" {
		f, _ := os.Create(*cpuprofile)
		pprof.StartCPUProfile(f)
		defer pprof.StopCPUProfile()
	}

	// Do the expensive stuff here
}
```

Then you can compile this program with `go build simple.go`, then run it with `./simple -cpuprofile=simple.prof`. This will output a `pprof` profile to `simple.prof`. The resulting file can be dragged into https://www.speedscope.app/, or opened directly with the CLI tool by running `speedscope simple.prof.`

# Importing via the `net/http/pprof` server profiling

The [`net/http/pprof`](https://golang.org/pkg/net/http/pprof/) package offers an easy-to-use profiling integration for long-lived servers.

If you have a server set up like this, you can download various different profiles by visiting the profile index page found at `http://localhost:$PORT/debug/pprof`. All of the available profile types should be importable into speedscope with the exception of `debug/pprof/trace`, which uses a different file format that speedscope doesn't yet support.

Rather than downloading the file and dropping it into https://www.speedscope.app/, if you have `speedscope` installed locally via `npm install -g speedscope`, you can also do e.g.:

```
curl http://localhost:$PORT/debug/pprof/profile?seconds=2 | speedscope -
```