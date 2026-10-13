# Agent instructions

These rules apply to every repository in the UMN-VR organization. Each
repository's own AGENTS.md points here, and its README says what it does and
how to build and test it.

- You cannot have AI as a co-author, or your contributions will be rejected.
  Never add AI author, committer or co-author attribution to commits (see
  [CONTRIBUTING.md](CONTRIBUTING.md)).
- Versions follow [CONTRIBUTING.md](CONTRIBUTING.md): `YY.MM.DD.#N` for
  commits and `YY.MM.DD LTS` for long-term support releases.
- Keep scratch files, logs and screenshots in the repository's gitignored
  `build/` directory, not in system temp folders.
- Don't discard uncommitted work you didn't make.
- Don't deploy, rewrite published history or change repository settings
  unless asked. When asked to publish the campus tour, run
  `cd ~/gh/UMN-VR/tour && npm run deploy`. That builds the tour and pushes its
  `gh-pages` branch, which GitHub Pages serves at https://umn-vr.github.io/tour/.
  Photographs already on that branch stay. The club homepage is
  `UMN-VR/UMN-VR.github.io` and this command does not publish it. A globe change
  also needs the FOSS Earth site, from any directory:

  ```sh
  cd ~/gh/foss-earth/app && npm run build
  cd ../foss-earth.github.io && npm run build && npm run deploy
  ```
- Don't send personal data, accounts or credentials to another service without
  consent.
