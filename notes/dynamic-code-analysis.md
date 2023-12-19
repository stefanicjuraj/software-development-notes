# Dynamic Code Analysis

Code analysis is the process of analyzing the software to discover additional insights about the software.

Analysis can be performed without running the program, in which case we are performing what is called **static code analysis**, in contrast to **dynamic code analysis**, which is performed on the software product during runtime, while the program is executing.

## Dynamic Code Analysis Purpose

- Detecting performance issues
- Detect program incorrectness
- Detect security vulnerabilities

Performance issues are caused by inefficient code. To improve application performance, we need to improve the code efficiency by reducing **resource consumption** and **completion time** as much as possible.

## Areas of Code Efficiency

### Memory

The active memory usage of your application while it's executing.

Memory efficiency does not always mean use as little memory as possible. That is often the case, but in some circumstances, it could mean exactly the opposite.

### Algorithm Efficiency

_Is there a different way the statements could have been written to accomplish exactly the same result, but faster? The sequence of operations you are choosing to accomplish a task. The thought process behind your statements. The order that they're in. The way they interact with each other._

_Using correct data types: is there a better built-in collection class that could be used? Are you making the most of the algorithms already found in the language (e.g. sorting algorithms)?_

### External Resource Usage - Disk Based Resources

Your application requires the use of some external resources. Some assets, something outside of the application itself. It's on the file system or in a database.

_How to minimize the amount of time that we want to read and write to that resource? Thinking about the best format we could save our data in, or the correct compression type we should use if we need to. How to reduce the amount of space that our assets take up on the drive?_

### Network Efficiency - Network Resources

This is an area that may be the most impactful to your application responsiveness if the app makes or receives network calls (e.g. using cloud storage, web services, peer to peer networking).

## Dynamic Code Analyzers

You don't know what the problem is until you measure it.

_An application has an issue, slow to start, slow to respond, slow to finish. The screen is freezing for a second or two, animations are jittery._

A user interface that freezes for a second might be experiencing a memory issue, or a threading issue, a network issue, an algorithm.

Dynamic Code Analyzers **monitor/measure various performance criteria** while the program is running. Performance analysis tools like **profilers** can:

- show **memory usage** - statistics on what kind of objects are taking up the most space
- show how much **CPU is being used**
- show what kind of activity is going on across **threads** if multi-threading is used

Profilers are not just measuring a snapshot of the application, its memory, its CPU, and so on, but rather, how it changes over a period of time.

![[task-monitoring-applications.png]]

---

[**`View Static Code Analysis`**](static-code-analysis)
[**`View Binary Code Analysis`**](binary-code-analysis)