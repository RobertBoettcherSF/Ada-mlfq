# Ada-mlfq
Ada implementation of a Multilevel Feedback Queue (MLFQ) scheduler

## Overview
This project implements a Multilevel Feedback Queue (MLFQ) scheduler in Ada. The MLFQ scheduler uses multiple priority queues with different time quanta to provide fair and efficient process scheduling.

## MLFQ Rules Implemented
1. **Rule 1 (Priority Preemption)**: If a higher priority queue has a job, it preempts the current running job
2. **Rule 2 (Round Robin)**: Within a queue, jobs run in round-robin fashion with a time quantum
3. **Rule 3 (New Job Entry)**: New jobs enter at the highest priority queue (queue 1)
4. **Rule 4 (Demotion)**: If a job uses its full time quantum, it gets demoted to the next lower queue
5. **Rule 5 (Aging)**: Periodically, all jobs are boosted back to the highest priority queue to prevent starvation

## Building and Running

### Prerequisites
- GNAT (GNU Ada compiler) - Part of GCC

### Installation
- **Linux (Debian/Ubuntu)**: `sudo apt-get install gnat`
- **macOS**: `brew install gnat`
- **Windows**: Download from [AdaCore](https://www.adacore.com/download)

### Run the Example Simulation
```bash
cd Ada-mlfq
gnatmake -P mlfq_project.gpr
./obj/main
```

### Run the Test Suite
```bash
cd Ada-mlfq
gnatmake -P mlfq_tests.gpr
./obj/mlfq_tests
```

The test suite includes 15 tests that verify:
- Empty scheduler behavior
- Single and multiple process completion
- Process demotion after quantum expiration
- Priority preemption (Rule 1)
- I/O yielding and blocking
- I/O wakeup after duration
- Aging and starvation prevention (Rule 5)
- Round Robin scheduling within queues
- Edge cases (zero CPU time, idle CPU, etc.)
- Different quantum values per queue

## Project Structure
- `main.adb` - Entry point that runs the example simulation
- `mlfq.ads` - Package specification with types and procedure declarations
- `mlfq.adb` - Package body with scheduler implementation
- `mlfq_project.gpr` - GPR project file for the main program
- `mlfq_tests.adb` - Comprehensive test suite
- `mlfq_tests.gpr` - GPR project file for the tests
- `obj/` - Build directory (automatically created)

## Scheduler Configuration
The scheduler can be configured with:
- Number of priority queues (up to 10)
- Time quantum for each queue
- Aging interval (set to 0 to disable aging)

## Example Output
The example simulation demonstrates three processes:
- Process 1: Long-running CPU-bound task (20 ticks)
- Process 2: Interactive I/O-bound task (5 ticks, yields every 1 tick, blocked for 3 ticks)
- Process 3: Medium-length task with occasional I/O (12 ticks, yields every 4 ticks, blocked for 2 ticks)

The simulation shows how processes are scheduled, preempted, demoted, and how I/O operations affect scheduling.
