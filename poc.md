ultracode - execute a spec by building an implementation from it.

THE SPEC IS AUTHORITATIVE. Read it first, in the order it specifies, before
writing any code. The spec made the decisions; do not re-make them, second-guess
them, or invent ones it left out. If the spec is silent, ambiguous, or
self-contradictory, Flag it and ask. Do not resolve it yourself.

INVOCATION
  ultracode <spec-entrypoint>  [target: <path>]  [mode: reference|production]
The entrypoint points to the spec file(s). Everything task-specific (file tree,
journey, decisions, scope, externals) lives in the spec, not in this skill.

MODE
- reference (default): a coherent, connected, exemplary implementation that
  TEACHES the pattern to less-senior developers. Clean, lightly commented. NOT
  for merge to master.
- production: same discipline, built to merge.
Both modes work on a branch, never master.

EXECUTION RULES (apply to any spec)
1. Honor scope exactly. Build what is in scope, exclude what is excluded, and
   never reintroduce an option the spec marked rejected or dead.
2. Follow the spec's named decisions exactly (its DD-x, ADRs, or decisions
   section). Do not substitute your own structure, routing, or patterns.
3. Prove the acceptance criteria. The spec lists what the implementation MUST
   demonstrate. The result must actually exercise each item, not just contain
   code for it. Do not claim a behavior you could not run.
4. Stub externals so nothing blocks the flow. For each external the spec names,
   hardcode a representative value and mark the seam:
     // TODO(impl): wire real <X> — stubbed for the reference architecture
   so every seam is an obvious hand-off checklist item.
5. Keep the responsibility split the spec defines (e.g. store / handler /
   component / service / config). Do not collapse layers.
6. Parity over polish. Match the spec's required behavior and contracts.
   Pixel-perfect or production UI is not a goal unless the spec says so.

HAND-OFF
When done, summarize what was built and list every TODO(impl) seam as a
checklist. Hand back for me to run locally and confirm it renders.


Example invocation:
ultracode spec.md
  read order: target-architecture -> gap-and-plan -> current-architecture
  target: local-modules/target-page/
  mode: reference
