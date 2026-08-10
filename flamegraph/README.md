# 🔥 FlameGraph — Linux Performance Profiling

A practical guide for collecting CPU profiling data with Linux `perf` and visualizing call stacks as an interactive **Flame Graph**.

Flame Graphs help identify CPU hotspots by showing where a process or the system spends its execution time.

This tool is useful for investigating:

* CPU-intensive functions
* unexpected performance bottlenecks
* expensive call paths
* application behavior under load
* system-level CPU consumption

> This directory contains a practical profiling workflow based on [`perf`](https://perf.wiki.kernel.org/) and the open-source [FlameGraph](https://github.com/brendangregg/FlameGraph) toolkit by Brendan Gregg.

---

## 🛠️ Requirements

The examples below assume a Debian/Ubuntu-based Linux system.

Install the required tools:

```bash
sudo apt update

sudo apt install \
    git \
    perl \
    linux-tools-common \
    linux-tools-$(uname -r) \
    -y
```

Clone the FlameGraph toolkit:

```bash
git clone https://github.com/brendangregg/FlameGraph.git
cd FlameGraph
```

---

# ⏺️ 1. Collect Profiling Data

Linux `perf` can record stack traces while a command or system is running.

### Profile a specific command

For example:

```bash
sudo perf record -g find /usr > /dev/null
```

This records CPU stack information while `find` is running.

The resulting profiling data is stored in:

```text
perf.data
```

### Profile the entire system

To capture system-wide activity for 10 seconds:

```bash
sudo perf record -a -g sleep 10
```

Where:

* `-a` — profile all CPUs / system-wide
* `-g` — collect call graphs
* `sleep 10` — defines the profiling window

---

# 🎨 2. Generate the Flame Graph

Convert the recorded `perf` data into a Flame Graph:

```bash
sudo perf script \
  | ./stackcollapse-perf.pl \
  | ./flamegraph.pl \
  > profile.svg
```

The pipeline consists of three stages:

```text
perf.data
    │
    ▼
perf script
    │
    ▼
Stack traces
    │
    ▼
stackcollapse-perf.pl
    │
    ▼
Folded stacks
    │
    ▼
flamegraph.pl
    │
    ▼
profile.svg
```

Open `profile.svg` in a browser to explore the result interactively.

---

# 🔍 3. Reading a Flame Graph

A Flame Graph represents the call stack of the profiled application or system.

### Vertical axis — stack depth

The Y-axis represents call-stack depth.

```text
        child function
             │
        parent function
             │
             ▼
          main()
```

Going upward means moving deeper into the call stack.

### Horizontal axis — samples

The X-axis represents the collected samples.

**Wider blocks indicate functions that account for more samples**, including time spent in functions called underneath them.

The horizontal position itself is generally not chronological.

---

# 🖱️ 4. Interactive Analysis

The generated SVG is interactive.

### Hover

Move the cursor over a block to see:

* function name
* stack information
* percentage of samples

### Zoom

Click a function to zoom into that part of the call tree.

### Search

Use:

```text
Ctrl + F
```

to search for a function or symbol.

Matching functions are highlighted, making it easier to locate specific code paths.

---

# 💡 Typical Workflow

A practical profiling workflow looks like this:

```text
Identify a performance question
            ↓
Choose a workload
            ↓
Run perf record
            ↓
Generate stack traces
            ↓
Create Flame Graph
            ↓
Identify hotspots
            ↓
Investigate the code path
            ↓
Optimize
            ↓
Profile again
```

The important part is not simply generating a graph, but **comparing profiling results before and after a change**.

---

# ⚠️ Notes

`perf` may require elevated privileges depending on the system's kernel configuration and `perf_event_paranoid` settings.

If profiling is restricted, check:

```bash
cat /proc/sys/kernel/perf_event_paranoid
```

System-wide profiling may require additional permissions.

The exact package names for `perf` can also vary between Linux distributions and kernel versions.

---

## 📚 References

* [Linux perf](https://perf.wiki.kernel.org/)
* [Brendan Gregg — Flame Graphs](https://www.brendangregg.com/flamegraphs.html)
* [FlameGraph on GitHub](https://github.com/brendangregg/FlameGraph)

---

## 📌 Status

Practical performance-profiling utility / reference workflow.

The goal of this tool is to keep a repeatable `perf` → Flame Graph workflow available for Linux performance investigations.
