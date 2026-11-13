# Turnover Model

A 4D steel and concrete turnover model you can scrub by date. Two schedule CSVs go in, steel by erection sequence and concrete by pour. The tool links them by where they sit on the grid, not by predecessor IDs, and shows every handoff between the trades.

Live page: https://fieldnotes.andrewwindisch.com/ai-research/turnover-model/

- One clock drives the 3D model, the LR 1300 crane picks, the concrete pump, the crews, the Gantt and the yardage released vs placed
- Handoffs are found from `Level` and grid extents. `Preds` is only read afterward to see whether the planner tied them
- Rules: foundations before raise (pour plus cure days), steel release before elevated pour, stacked trades, pump and crane in the same bay, missing logic ties
- Explode the job by sequence and pour, isolate one group, cut a section, toggle crews
- Slip any sequence or pour from the detail panel or by dragging its Gantt bar and watch the downstream handoffs recompute
- Ghost compares what is in place against a baseline (original dates, a snapshot, or a second CSV pair). Float colors every group by the days of air on its tightest handoff. Hook cam rides the jib
- Single static file (`index.html`), Three.js r147 from jsDelivr. Works on GitHub Pages or any static host. `?preview=1` gives a full-bleed model with no controls for embeds

## Bring your own schedules

Load a steel CSV and a concrete CSV on the Data & rules tab. Both share one column set. The sample files in `sample/` show the format.

| Column | What it is |
| --- | --- |
| `ID, Activity, Trade, Group` | Group = erection sequence (steel) or pour (concrete). Rollup unit |
| `Level` | FND, B1, L1 ... RF. Elevated pours and deck releases must share a level to match |
| `GridX0, GridX1, GridY0, GridY1` | Grid extents by label. Zero width (a wall on grid E) matches anything touching that line |
| `Start, Finish, Dur, Preds` | ISO dates, workdays, `ID;ID+2;ID-1` |
| `Type, Role` | task / milestone. Role drives the rules: `raise`, `deck`, `release`, `pour`, `pad`, `shakeout` |
| `Ref` | Optional sheet numbers and member callouts shown when you tap a group |

## Sample set

Grid and framing are based on public 2019 bid drawings for the OSU College of Osteopathic Medicine at the Cherokee Nation in Tahlequah, Oklahoma (Bid Package 03 Foundations and the Bulk Steel Package, posted on cherokeebids.org). Structural: Chavez-Grieves. Architect: James R. Childers Architect. Nothing from the sheets is reproduced here. The schedules, quantities and conflicts are hypothetical.

Crane capacities interpolate the Liebherr LR 1300 SX reference chart (luffing jib No. 2316) for demonstration only. This is a learning model, not a lift plan or a project schedule.

By Andrew Windisch. https://www.linkedin.com/in/andrewwindisch
