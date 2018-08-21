[`perf`](https://perf.wiki.kernel.org/index.php/Main_Page) is a tool for profiling on linux.

You can import profiles into speedscope which were recorded using `perf record` and formatted using `perf script`.

    perf record -a -F 999 -g -p PID > perf.data
    perf script -i perf.data > profile.linux-perf.txt

Then drop the resulting `perf.txt` into speedscope, or if you have speedscope installed
locally, you can run:

    perf record -a -F 999 -g -p PID > perf.data
    perf script -i perf.data | speedscope -