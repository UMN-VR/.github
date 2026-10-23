# Task-specific agent guidance

Read only the sections selected by [AGENTS.md](AGENTS.md). These are the
full organization rules, moved out of the always-read entry point.

## History

When given a previous agent's local JSONL conversation, use the shared
[conversation reader](https://github.com/foss-earth/docs/blob/main/docs/agent-conversations.md):
`node ~/gh/foss-earth/docs/scripts/read-agent-conversation.mjs <file> --prompts --all`,
then search or read a bounded tail. It supports Claude and Codex logs without
dumping snapshots or reasoning. Verify historical claims against today's code.

## Contributions

- You cannot have AI as a co-author, or your contributions will be rejected.
  Never add AI author, committer or co-author attribution to commits (see
  [CONTRIBUTING.md](CONTRIBUTING.md)).

- Versions follow [CONTRIBUTING.md](CONTRIBUTING.md): `YY.MM.DD#N` for
  commits and `YY.MM.DD LTS` for long-term support releases.

## Workspace

- Keep scratch files, logs and screenshots in the repository's gitignored
  `build/` directory, not in system temp folders.

- Don't discard uncommitted work you didn't make.

- Don't send personal data, accounts or credentials to another service without
  consent.

## Maps and prepared data

- **Google Maps key:** before asking for a key, check `GOOGLE_3D_TILES_KEY`
  in the environment and ignored `.env.local` files in `~/gh/foss-earth/app`,
  `~/gh/UMN-VR/tour`, and `~/gh/0sfs/fly`. `FOSS_EARTH_GOOGLE_KEY` remains a
  legacy fallback. Either environment name beats files; the new name beats the
  legacy name across files. Read only these named variables; never
  print the key in agent logs or commit the file. The user-facing `npm run dev`
  startup intentionally includes `gkey` in its local/network URLs and QR; agents
  use `npm run llm-dev` to omit it. Build-time photo height preparation uses
  Google 3D geometry first; another source is a recorded fallback only.

- **Prefer build-time work over runtime work.** Prepare stable placement heights
  explicitly, record their source, and consume fixed scene values at runtime.
  Never move photos as map LOD changes. Populate and validate every consuming
  scene before removing a legacy placement path; do not leave orbs unplaced.

## Publishing

- Never push source or publish/deploy unless the user explicitly requests that
  specific remote action. Source-push permission is not deployment permission.
  Prepare changes locally and let the user test them before publication;
  automated checks and agent browser tests do not replace that user review.
  A prototype URL/path or a repository-creation request is not permission to push.

- Don't deploy, rewrite published history or change repository settings
  unless asked. When asked to publish the campus tour, run
  `cd ~/gh/UMN-VR/tour && npm run deploy`. That builds the tour, when its
  `gh-pages` branch lacks the build this would make, and pushes that branch,
  which GitHub Pages serves at https://umn-vr.github.io/tour/.
  Photographs already on that branch stay. The club homepage is
  `UMN-VR/UMN-VR.github.io` and this command does not publish it. A globe change
  also needs the FOSS Earth site, from any directory:

  ```sh
  cd ~/gh/foss-earth/foss-earth.github.io && npm run deploy
  ```

## UI

- New UI and controls belong in the app's tabs. Create a new tab unless the user
  asks for an existing tab. Do not add a top bar, floating panel or overlay plate
  unless the user explicitly asks for that layout. Reuse the existing tab APIs.

- **Explanation on demand:** use a compact **?** button by default for
  supplementary information, diagnostics and rationale, rather than a wordy
  Details/More info action. Keep it last and available on collapsed components.
  Keep only essential terse state, errors/fallbacks,
  pending/apply feedback and decision-critical instructions visible by default.
  Do not hide information needed to understand the current state or avoid mistakes.

- **Readable control phrases:** choose label/control order by grammatical
  sense, usually `Implementation [TS / WASM] ?`. Prefix/suffix text is allowed;
  do not impose a universal slider-first or label-first order. Keep help last.

- **Paragraph grouping:** each logical component in a paragraph grid has its
  own compact rounded rectangle by default, including collapsed component
  overrides. Keep a choice's segments together inside one track within its group.
  Expanded component/group titles are the first naturally sized item in the
  same wrapping paragraph grid as their controls, not a separate header row.
  Full section headings are the exception and can occupy their own row.
  Paragraph grids with expandable items show expanded items first, then
  minimized items, using an order override that preserves relative order
  within each group and retains focus/control state.

- **Compact controls:** arrange content as compactly as practical, using natural
  widths and wrapping paragraph grids where useful. Discrete choices use one
  rounded segmented slider with short text buttons (digits for counts: 1
  worker), selected by fill/outline; no visible radio circles. Use **Global /
  Auto / Manual**. The **?** button is last; source-link icons belong inline at
  the end of its tooltip text, never in another row button. Prefer existing
  recognizable icons over verbose action text, with accessible names. Reuse the
  shared UI factory and follow the full [control design
  spec](https://github.com/foss-earth/docs/blob/main/docs/ui-layout.md#compact-segmented-choices).

## Browser testing

- **Stranded Chrome clones:** a run of the installed Google Chrome that is
  killed instead of closed leaves a copy of the app, about 2 GB by `du`, under
  `/private/var/folders`. After a Chrome run you stopped, that timed out or that
  crashed, and whenever disk space comes up, run
  `~/gh/foss-earth/browser-testing/scripts/chrome-clones.sh --clean`. It keeps
  the clones of running browsers.
  [chrome-code-sign-clones.md](https://github.com/foss-earth/docs/blob/main/docs/validation/chrome-code-sign-clones.md)
  says why they appear.

## Camera and input

- **Physical UX:** camera and 360 image navigation must feel like a physical
  object with mass, momentum, and direct contact. Follow
  [foss-earth/docs/docs/physical-ux.md](https://github.com/foss-earth/docs/blob/main/docs/physical-ux.md)
  and [foss-earth/docs/docs/camera-motion.md](https://github.com/foss-earth/docs/blob/main/docs/camera-motion.md).
