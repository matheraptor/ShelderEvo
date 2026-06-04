# RMMZ integration plan

## GOAL

Develop a new prototypal client for [MAGPIE_Server](../../MAGPIE_Server/README.md), using the [ShelderEvo codebase](../../HASTRAL/03_MEMORY/wiki/shelderevo_prototype/index.md) and MAGPIE legacy files as reference for logic and inspiration rather than a direct foundation.

### Conditions for success

- **Must be a functional client that connects to the existing server**
  - *Integrate with existing account handling logic*
  - *Integrate with existing CLI logic*
- **Must use RPG Maker MZ (RMMZ) engine**
- **Must use Myth Atelier CGC (Card Game Combat) plugin**
- **Must use copyright-free assets**
- **Must have at least the core gameplay loop**
  - *adopt creature embryo*
  - *creature trait generation from species template and evolution mechanic*
  - *creature growth until death, either from aging or damage*
  - *player influence creature by 'suggesting' card-play*
  - *Evolution Points (EVP) collection through evolution-related quests*
- **Must be a standalone NWjs app dowloadable via itch.io**
- **Must follow and maintain the overall ShelderEvo theme and aesthetics**
  - *strictly adhere to [ShelderEvolution meta](https://matheraptor.notion.site/Shelder-Evolution-0cea90cc42694d6da94c2f9cee477ec0)*
  - *strictly adhere to guidelines in [README](../../MAGPIE_Server/README.md)*
  - *strictly use existing custom assets and avoid copyrighted material*

---

- [ ] MISSION 1: RECON -- pattern extraction and snippet harvesting
  - [ ] TASK 1: extract viable logic/snippets from Project_L2e/ codebase
    - [ ] STEP: identify and harvest Trait Generation logic
    - [ ] STEP: identify and harvest Evolution/Growth mechanics
    - [ ] STEP: extract Embryo adoption flow
  - [ ] TASK 2: extract viable logic/snippets from MAGPIE/ codebase
    - [ ] STEP: harvest legacy socket event handlers
    - [ ] STEP: extract any existing creature-related data schemas
  - [ ] TASK 3: consolidate [INTEL](../docs/intel.md) as a reference library
    - [ ] STEP: map extracted snippets to ShelderEvo target files
    - [ ] STEP: document compatibility issues with NWjs/RMMZ

---

- [ ] MISSION 2: PREP -- prepare an implementation plan
  - [ ] TASK 1: use INTEL to update this plan
  - [ ] TASK 2: schedule work within June 8th 08:00 deadline
  - [ ] TASK 3: allocate resources

---

- [ ] MISSION 3: client boot
  - [ ] TASK: inherit "CLI" style and logic from server/public/cli/
    - [ ] STEP 1: link [cli.js](../js/cli/cli.js) to [index.html](../index.html)
    - [ ] STEP 2: add the script tag to [HTML entry point](../index.html)
  - [ ] TASK: namespace alignment
    - [ ] STEP: ensure `MAGPIE_CLI` in [cli.js](../js/cli/cli.js) correctly references `MAGPIE.SOCKET` and `MAGPIE.meta` from [MAGPIE.js](../js/MAGPIE.js)
    - [ ] STEP: TUI `printLine` and `switchModule` must target `#terminal-output` and `#crt-screen` in [HTML](../index.html)
  - [ ] TASK: socket handshake
    - [ ] STEP: connection check in `MAGPIE_CLI.initSocket()`
    - [ ] STEP: token validation `localStorage.getItem("jwt_token")` on boot
  - [ ] TASK: Auth routing
    - [ ] STEP: if token is valid => skip to `root` module => trigger `updater`
    - [ ] STEP: if token is missing/invalid => `switchModule('account')` => prompt for `login`
  - [ ] TASK: login
    - [ ] STEP: `LOGIN` emit in `stepHandlers.login_password`
    - [ ] STEP: handle `LOGIN_SUCCESS` response to store JWT
  - [ ] TASK: updater
    - [ ] STEP: hook `LOGIN_SUCCESS` event in [cli.js](../js/cli/cli.js) to call `MAGPIE.BOOT.updater()`
    - [ ] STEP: `MAGPIE.BOOT.updater` to compare local vs server
    - [ ] STEP: asset sync *(placeholder/basic)*
    - [ ] STEP: signal sync success
    - [ ] STEP: use `MAGPIE_CLI.printLine` to notify user
  - [ ] TASK: handoff to RMMZ [main.js](../js/main.js)
    - [ ] STEP: implement `HandoffManager` to bridge TUI state to RMMZ global object
    - [ ] STEP: transfer state `jwt_token` and `playerID` to be available within RMMZ engine for session persistence
    - [ ] STEP: UI transition from [CLI html](../js/cli/index.html) to [RMMZ html](../js/main.html)
    - [ ] STEP: execute DOM purge (remove TUI CSS/HTML) to prevent visual artifacts
    - [ ] STEP: [boot engine](../js/main.js)

---
