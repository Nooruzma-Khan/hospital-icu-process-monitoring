# Hospital ICU Process Monitoring

An interactive, single-page **Operating System simulation** in which every ICU patient is a monitor *process*.
It demonstrates process management, CPU scheduling, deadlock avoidance, memory management and file allocation
using a hospital ICU as the running example.

> Operating System micro-project (course code 315319) · Diploma in Computer Engineering, Vidyalankar Polytechnic · by **Nooruzma Khan**
>
> Educational simulation only. No real patient data is used and no real medical equipment is controlled.

**Live demo:** _add your Vercel link here_

## Features

The app has three pages plus a ward overview, a live ECG trace and a kernel event log that are visible on every page.

| Page / section | OS concept | Course outcome |
| --- | --- | --- |
| **Admit patient** | Process creation (New → Ready), PID, priority and burst derived from the patient's condition, first vitals file written | CO2 |
| **Patient records** | Retrieve a vitals file by Patient ID / PID / name through its index block, add readings, discharge (terminate process) | CO5 |
| **Lab – System information** | Kernel info, simulator uptime, memory in use, OS services mapped to the ICU, process state summary | CO1 |
| **Lab – Processes** | Process table, Process Control Block, state transitions, IPC message queue to the Alarm Manager (a critical alarm raises the sender's priority) | CO2 |
| **Lab – Scheduling** | Priority (non-preemptive) vs Round Robin with Gantt charts, completion, turnaround and waiting time | CO3 |
| **Lab – Deadlock** | Banker's algorithm: Need matrix, safe sequence, resource-request test for ECG monitors, ventilators and infusion pumps | CO3 |
| **Lab – Memory** | First / Best / Worst Fit partition allocation with internal fragmentation; FIFO vs LRU page replacement | CO4 |
| **Lab – Files** | Indexed allocation on a 32-block disk (index block holds at most 8 pointers), retrieval by Patient ID | CO5 |

## Run it

No build step and no dependencies. Open `index.html` in Chrome or Edge, or serve the folder:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

All data lives in the browser's memory, so the five sample patients are restored when the page is reloaded.

## Sample results (default data)

| Module | Result |
| --- | --- |
| Priority scheduling | Average waiting time 5.80, average turnaround time 9.80 |
| Round Robin (quantum 2) | Average waiting time 8.80, average turnaround time 12.80 |
| Banker's algorithm, available (3, 3, 2) | Safe sequence PT-102 → PT-104 → PT-105 → PT-101 → PT-103 |
| Request PT-101 (1, 0, 2) | Denied – would lead to an unsafe state |
| First Fit, partitions 100/500/200/300/600 KB | PT-104 (426 KB) waits; internal fragmentation 569 KB |
| Best Fit / Worst Fit | 443 KB, all placed / 769 KB, PT-104 waits |
| FIFO, 3 frames, `7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1` | 15 page faults (hit ratio 25%) |
| LRU, same string | 12 page faults (hit ratio 40%) |

## Repository layout

```
index.html                          the complete simulation (HTML + CSS + JavaScript, self-contained)
```

## Deploy on Vercel

Import this repository at https://vercel.com/new. Framework preset: **Other**. Leave build and output settings empty; Vercel serves `index.html` as a static site.
