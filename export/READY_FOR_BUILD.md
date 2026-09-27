# Ready for build

Tasks here are fully specified — zero decisions left for the build agent. Copy each one into the build repo's `TASKS.md` once you've moved it over, then delete it from here (this file should stay short — it's a queue, not an archive).

---

## Example (delete once you have real ones)

- [ ] Implement `POST /rooms/:id/join` — see `decisions/0003-room-membership.md` for the contract. Returns 200 + player object on success, 409 if room full, 404 if room doesn't exist.
  - Acceptance: hitting join on a full room returns 409 and does not modify state.
