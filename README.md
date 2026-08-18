# Timer Fix — TBI Technical Team Selection Task

## Overview

This repository contains my solution for the TBI Technical Team selection task.

The task has two parts:

* **Part 1:** Fix the bugs in the provided countdown timer.
* **Part 2:** Add pause/resume functionality and make the timer resistant to delays caused by browser backgrounding or system sleep.

## Files

```text
timer-fix/
├── README.md
├── original.html
├── part1.html
└── part2.html
```

### `original.html`

The original buggy timer provided in the task.

### `part1.html`

The bug-fixed version.

Fixes include:

* Preventing multiple intervals when Start is clicked repeatedly.
* Displaying seconds with a leading zero (`09` instead of `9`).
* Stopping the countdown at `00:00`.
* Properly clearing the active interval.

### `part2.html`

The final version with:

* Start functionality.
* Pause/resume functionality.
* Protection against multiple intervals.
* Timestamp/deadline-based countdown.
* Correct behavior after browser tab backgrounding or laptop sleep.
* Timer stopping correctly at zero.

## Key Design Decision

In Part 1, the countdown is updated using:

```javascript
timeLeft--;
```

This assumes that every interval callback represents exactly one second.

However, browser timers can be delayed or throttled when a tab is inactive or the computer goes to sleep.

For Part 2, I therefore use a deadline as the source of truth:

```text
remaining time = deadline - current time
```

The interval is only used to refresh the display. It is not used to measure elapsed time.

This prevents timer drift when JavaScript callbacks are delayed.

## Testing

I tested the timer for:

* Multiple Start clicks.
* Pause and Resume.
* Switching browser tabs.
* Reaching `00:00`.
* Preventing negative time.
* Delayed browser execution.
* Laptop sleep/wake behavior.

## How to Run

No dependencies are required.

Open either `part1.html` or `part2.html` directly in a browser.



The main engineering decision in Part 2 is separating **time measurement** from **UI updates**.

`setInterval()` is not treated as the clock. The actual remaining time is calculated from timestamps, while the interval only refreshes the displayed value.
