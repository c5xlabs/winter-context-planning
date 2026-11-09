# Deliver an epic

Mark an epic delivered and archive it, in one change. Use it once there is evidence the epic reached its users. Each
step applies the rule it cites; this is only the order of work, and every step lands in the same commit.

1. **Set the status.** In the epic's `epic.md`, set `status: delivered` — `preq:epic-status`. Leave `refinement:` alone;
   only the product owner grades it.
2. **Move the folder.** `git mv` the epic folder from `work/` to `delivered/`, keeping its shape; when it is the last
   live epic of its initiative, move the rest of the initiative folder too — `preq:delivered-archive`.
3. **Repoint links.** Fix every relative link into or out of the moved folder. Ids need no change —
   `preq:delivered-archive`.
4. **Drop the registry row.** Remove the epic's row from `epics.md` — `preq:epic-registry`. When its initiative is now
   fully delivered, point the initiative's row in `initiatives.md` into `delivered/` — `preq:initiative-registry`.
5. **Update the charts.** In every milestone chart naming the epic, or an initiative it completes, set the cell to
   `delivered` — `preq:milestone-registry`.
6. **Record the ledger.** Move each milestone whose chart is now all `delivered` from `milestones.md` into
   `delivered.md`, newest first, its Status column replaced by Notes; when the epic serves no milestone, add it under
   `## Outside the milestones` — `preq:delivery-ledger`.
7. **Check.**
   - The epic's folder sits in `delivered/`, and no epic left in `work/` says `status: delivered`.
   - `epics.md` has no row for it, every chart naming it says `delivered`, and no reached milestone is left in
     `milestones.md`.
   - Every relative link into or out of the moved folder resolves.
8. **Commit** as a `chore` scoped by the epic id, its body saying the epic was delivered and archived —
   `preq:commit-messages` in [contributing.md](../contributing.md).
