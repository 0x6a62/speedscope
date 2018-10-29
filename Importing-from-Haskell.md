GHC provides built in profiling support that can export a JSON file.
In order to do this you need to compile your executable with profiling
support and then pass the `-pj` RTS flag to the executable.

This will produce a `my-binary.prof` file in the current directory which
you can import into speedscope.

## Using GHC

See the [GHC manual page on profiling](https://downloads.haskell.org/~ghc/latest/docs/html/users_guide/profiling.html)
for more extensive information on the command line flags available.

```
$ ghc -prof -fprof-auto -rtsopts Main.hs
$ ./Main +RTS -pj -RTS
```

## Using Stack

### With executables

```
$ stack build --profile
$ stack exec -- my-executable +RTS -pj -RTS
```

### With tests

```
stack test --profile --test-arguments "+RTS -pj -RTS"
```