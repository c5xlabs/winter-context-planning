# Deliver an epic

Once there is evidence an epic reached its users, mark it delivered and archive it. All of the steps below land in one
commit.

1. In the epic's `epic.md`, set `status: delivered`. Leave `refinement:` alone; only the product owner grades it.
2. `git mv` the epic folder from `work/` to `delivered/`, within its project in a repo with projects, keeping its shape.
   If it was the initiative's last live epic, move the rest of the initiative folder too.
3. Fix every relative link into or out of the moved folder. Ids don't change.
4. If its initiative is now fully delivered, point the initiative's row in `initiatives.md` into `delivered/`.
5. In every milestone chart naming the epic, or an initiative it completes, set the cell to `delivered`.
6. Move each milestone whose chart is now all `delivered` from its `milestones.md` into the `delivered.md` beside it,
   newest first, with the Status column replaced by Notes. An epic that serves no milestone goes under
   `## Outside the milestones` in its project's ledger instead.
7. Check that no epic left in `work/` says `status: delivered`, no reached milestone is left in `milestones.md`, and
   every moved link resolves.
8. Commit as a `chore` scoped by the epic id, with a body saying the epic was delivered and archived
   ([`../contributing.md`](../contributing.md)).
