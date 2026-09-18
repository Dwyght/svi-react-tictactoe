# SVI Tic-Tac-Toe — React Project Structure

## Overview

This repository defines the proposed **React + TypeScript project structure** for migrating the existing vanilla JavaScript Tic-Tac-Toe application.

The goal is not to create a one-to-one copy of the old folders. The structure reorganizes the application based on React responsibilities and corrects parts of the existing organization that would become difficult to maintain as the application grows.

The main approach is **domain-first, then technical type**. The major application domains are `home`, `game`, and `history`. Each feature owns the components, hooks, API modules, services, state, utilities, and types that are specific to it. Code used by multiple features stays in shared top-level folders.

The target structure uses:

- React with TypeScript (`.tsx` / `.ts`)
- Vite
- React Router for page navigation
- Zustand for application state where shared state is needed
- CSS Modules with centralized styles under `src/styles/`

---

## Before and After Project Structure

### BEFORE — Existing Vanilla JavaScript Application

```text
svi-js-tic-tac-toe/
├── src/
│   ├── assets/
│   │   └── images/
│   │       ├── emote/
│   │       ├── loading-sushis/
│   │       ├── o-sushis/
│   │       └── x-sushis/
│   ├── css/
│   │   ├── base/
│   │   │   ├── layout.css
│   │   │   ├── reset.css
│   │   │   └── tokens.css
│   │   ├── components/
│   │   ├── pages/
│   │   │   ├── game-page.css
│   │   │   ├── history-page.css
│   │   │   └── home-page.css
│   │   ├── main.css
│   │   └── responsive.css
│   └── js/
│       ├── api/
│       │   ├── tictactoeApi.js
│       │   └── webserviceApi.js
│       ├── components/
│       │   ├── base/
│       │   │   ├── Button.js
│       │   │   ├── Card.js
│       │   │   ├── ConfirmModal.js
│       │   │   └── Modal.js
│       │   ├── game/
│       │   │   ├── Board.js
│       │   │   ├── CreateGameModal.js
│       │   │   ├── EmotePicker.js
│       │   │   ├── HowToPlayModal.js
│       │   │   ├── JoinGameModal.js
│       │   │   ├── PauseMenu.js
│       │   │   ├── ResultModal.js
│       │   │   ├── ResumeGameModal.js
│       │   │   ├── Scoreboard.js
│       │   │   ├── SpectateModal.js
│       │   │   └── SushiSelector.js
│       │   ├── history/
│       │   │   └── HistoryReplay.js
│       │   ├── ConveyorBelt.js
│       │   ├── ScreenManager.js
│       │   └── SplashScreen.js
│       ├── config/
│       │   └── constants.js
│       ├── game/
│       │   ├── boardLogic.js
│       │   └── gameCode.js
│       ├── pages/
│       │   ├── Emote.js
│       │   ├── Game.js
│       │   ├── History.js
│       │   ├── Home.js
│       │   ├── Quit.js
│       │   └── Result.js
│       ├── services/
│       │   ├── gameFlowService.js
│       │   ├── playerTabLockService.js
│       │   ├── pollingService.js
│       │   ├── storageService.js
│       │   └── waitingRoomFlow.js
│       ├── state/
│       │   └── gameState.js
│       ├── utils/
│       │   ├── clipboard.js
│       │   ├── dom.js
│       │   └── sushi.js
│       └── app.js
├── test/
├── README.md
└── index.html
```

The existing JavaScript application already has architectural separation through folders such as `components`, `pages`, `services`, `api`, `state`, `config`, and `utils`. These are valid responsibilities that are also useful in a React application. However, most of the old structure is grouped by **technical type first**, so files that belong to one domain can be spread across several top-level folders.

### AFTER — Proposed React + TypeScript Application

```text
svi-react-tic-tac-toe/
├── public/
│   ├── assets/
│   │   ├── app/
│   │   │   └── loading-sushis/
│   │   ├── game/
│   │   │   ├── emote/
│   │   │   ├── o-sushis/
│   │   │   └── x-sushis/
│   │   └── home/
│   └── favicon.png
├── src/
│   ├── app/
│   │   ├── layout/
│   │   │   ├── AppLayout.tsx
│   │   │   ├── BackgroundVideo.tsx
│   │   │   └── ConveyorBelt.tsx
│   │   ├── providers/
│   │   │   └── AppProviders.tsx
│   │   ├── splash/
│   │   │   └── SplashGate.tsx
│   │   └── NotFoundPage.tsx
│   ├── components/
│   │   ├── Button/
│   │   │   └── Button.tsx
│   │   ├── Card/
│   │   │   └── Card.tsx
│   │   ├── ConfirmModal/
│   │   │   └── ConfirmModal.tsx
│   │   ├── CopyableCode/
│   │   │   └── CopyableCode.tsx
│   │   └── Modal/
│   │       ├── Modal.tsx
│   │       └── ModalContext.tsx
│   ├── config/
│   │   ├── constants.ts
│   │   └── env.ts
│   ├── features/
│   │   ├── game/
│   │   │   ├── api/
│   │   │   │   ├── sessionApi.ts
│   │   │   │   └── tictactoeApi.ts
│   │   │   ├── components/
│   │   │   │   ├── Board.tsx
│   │   │   │   ├── Cell.tsx
│   │   │   │   ├── EmotePicker.tsx
│   │   │   │   ├── PauseMenu.tsx
│   │   │   │   ├── QuitConfirmModal.tsx
│   │   │   │   ├── ResultBanner.tsx
│   │   │   │   ├── ResultModal.tsx
│   │   │   │   ├── ResumeGameModal.tsx
│   │   │   │   ├── Scoreboard.tsx
│   │   │   │   ├── SushiSelector.tsx
│   │   │   │   └── TurnIndicator.tsx
│   │   │   ├── hooks/
│   │   │   │   ├── useGamePolling.ts
│   │   │   │   ├── useGameSession.ts
│   │   │   │   ├── usePlayerTabLock.ts
│   │   │   │   └── useResumeGamePrompt.ts
│   │   │   ├── pages/
│   │   │   │   └── GamePage.tsx
│   │   │   ├── services/
│   │   │   │   ├── boardService.ts
│   │   │   │   ├── gameSessionService.ts
│   │   │   │   └── scoreboardService.ts
│   │   │   ├── store/
│   │   │   │   └── gameStore.ts
│   │   │   ├── utils/
│   │   │   │   ├── boardLogic.ts
│   │   │   │   └── gameCode.ts
│   │   │   └── types.ts
│   │   ├── history/
│   │   │   ├── api/
│   │   │   │   └── historyApi.ts
│   │   │   ├── components/
│   │   │   │   ├── HistoryReplay.tsx
│   │   │   │   ├── PlayerHistoryView.tsx
│   │   │   │   ├── RoomHistoryView.tsx
│   │   │   │   └── RoundHistoryView.tsx
│   │   │   ├── hooks/
│   │   │   │   └── useHistoryData.ts
│   │   │   ├── pages/
│   │   │   │   └── HistoryPage.tsx
│   │   │   ├── utils/
│   │   │   │   └── historyFormatting.ts
│   │   │   └── types.ts
│   │   └── home/
│   │       ├── components/
│   │       │   ├── CreateGameModal.tsx
│   │       │   ├── HomeNotice.tsx
│   │       │   ├── HowToPlayModal.tsx
│   │       │   ├── JoinGameModal.tsx
│   │       │   └── SpectateModal.tsx
│   │       ├── hooks/
│   │       │   └── useWaitingRoom.ts
│   │       ├── pages/
│   │       │   └── HomePage.tsx
│   │       └── types.ts
│   ├── hooks/
│   │   ├── useClipboard.ts
│   │   └── useLocalStorage.ts
│   ├── services/
│   │   ├── httpClient.ts
│   │   └── storageService.ts
│   ├── store/
│   │   └── sessionStore.ts
│   ├── styles/
│   │   ├── app/
│   │   ├── components/
│   │   ├── features/
│   │   │   ├── game/
│   │   │   ├── history/
│   │   │   └── home/
│   │   ├── global.css
│   │   ├── layout.css
│   │   ├── reset.css
│   │   ├── responsive.css
│   │   └── tokens.css
│   ├── types/
│   │   └── index.ts
│   ├── App.tsx
│   ├── main.tsx
│   ├── router.tsx
│   └── vite-env.d.ts
├── .env.example
├── .eslintrc.cjs
├── .gitignore
├── .prettierrc
├── index.html
├── package.json
├── tsconfig.json
└── vite.config.ts
```

The React structure preserves the useful separation already present in the JavaScript application, but reorganizes domain-specific code under `features/home`, `features/game`, and `features/history`. Technical folders such as `components`, `hooks`, `api`, and `services` then exist inside the domain that owns them. Shared code remains at the top level only when it is genuinely reused across features.

Static asset files are omitted from the trees because individual images and videos do not affect the architectural comparison.

---

## How the React Structure Works

The folder structure also reflects how responsibilities flow through the React application:

```text
User Action
    ↓
Route / Page
    ↓
Component
    ↓
Hook
    ↓
Service / API
    ↓
Backend or Store
    ↓
Updated State
    ↓
React re-renders the affected UI
```

A route loads the appropriate feature page, such as `GamePage.tsx`. The page coordinates the components needed for that screen. Components handle presentation and user interaction, while hooks manage React-specific behavior and lifecycle concerns such as polling or session handling. Services contain application operations, API modules communicate with the backend, and stores hold shared state when needed. When state changes, React re-renders the affected components.

For example, a Game interaction can follow this responsibility flow:

```text
GamePage
    ↓
Board
    ↓
useGameSession
    ↓
gameSessionService
    ↓
tictactoeApi
    ↓
Backend
```

This separation keeps UI, React lifecycle behavior, application logic, and backend communication in distinct responsibilities instead of combining them in one file.

---

## Architecture

### Domain first, technical type second

The existing JavaScript application already has useful architectural separation through folders such as `components`, `pages`, `services`, `api`, `state`, `config`, and `utils`. These concepts also make sense in a React application, so they are not discarded.

The main change is **where domain-specific code is placed**.

In the old structure, code is primarily grouped by technical type. A single feature such as Game can therefore be spread across `pages`, `components`, `services`, `api`, `state`, and utility folders.

In the React structure, the application is grouped first by domain:

```text
features/
├── home/
├── game/
└── history/
```

Each domain is then divided by technical responsibility only when needed:

```text
features/game/
├── api/
├── components/
├── hooks/
├── pages/
├── services/
├── store/
├── utils/
└── types.ts
```

This keeps related code together. A developer working on Game can find most Game-specific code inside one feature folder instead of moving between several unrelated top-level folders.

It also reduces code concentration in large files. Responsibilities that were previously handled together can be separated into smaller components, hooks, services, and utilities. This makes each file more focused and reduces the amount of code that needs to be read or changed for a single responsibility.

---

## Folder Responsibilities

| Folder | Responsibility |
|---|---|
| `src/app/` | Application-wide shell concerns such as layout, providers, splash behavior, and the not-found page. |
| `src/features/` | Domain-specific code grouped by Home, Game, and History. |
| `src/components/` | Reusable UI components that are not owned by one feature. |
| `src/hooks/` | Reusable React hooks shared by multiple features. |
| `src/services/` | Shared infrastructure such as HTTP and browser storage access. |
| `src/store/` | State that must be shared across multiple features. |
| `src/config/` | Constants and environment configuration. |
| `src/types/` | Types shared across domains. |
| `src/styles/` | Centralized styles organized to mirror the application structure. |
| `public/assets/` | Static assets grouped by their application domain. |

A file should remain inside a feature when it is only used by that feature. It should move to a shared top-level folder only when multiple features genuinely need it.

---

## Important Changes from the JavaScript Application

| Existing JavaScript approach | React structure | Reason for the change |
|---|---|---|
| Technical folders such as `components`, `pages`, `services`, and `api` contain files from different domains. | Domain folders under `features/`, then technical folders inside each feature. | Keeps related files together and makes feature ownership clearer. |
| Components manually create and update DOM elements. | React function components with JSX. | UI becomes declarative and is updated from React state instead of manual DOM operations. |
| `ScreenManager` controls which screen is displayed. | React Router handles Home, Game, History, and invalid routes. | Pages become real routes and navigation is handled by the routing layer. |
| Some files combine UI, state handling, polling, API calls, and other responsibilities. | Responsibilities are separated into components, hooks, API modules, services, stores, and utilities. | Reduces code in individual files and makes each part easier to understand and maintain. |
| `gameState.js` is a shared mutable state object. | Feature and application stores such as `gameStore.ts` and `sessionStore.ts`. | Gives shared state a clear owner and predictable update mechanism. |
| Polling and browser lifecycle behavior are manually started and stopped. | Custom hooks such as `useGamePolling` and `usePlayerTabLock`. | React lifecycle logic stays with the behavior that owns it and can clean itself up when the component unmounts. |
| Some files named as pages represent modal or in-game behavior rather than navigable screens. | Only route-level screens use the `Page` name; modal behavior becomes components. | Gives `Page` a clear meaning in the React application. |
| One API module can serve multiple unrelated domains. | API modules are separated by feature, such as `sessionApi.ts` and `historyApi.ts`. | Keeps API ownership aligned with the feature using it. |
| Backend URLs are stored with application constants. | Environment-specific values are read through `config/env.ts`. | Allows different backend URLs without changing source code. |
| Plain JavaScript is used throughout. | TypeScript is used for components, services, APIs, state, and domain types. | Adds compile-time checking for application data and function contracts. |
| Styles are maintained in a separate CSS hierarchy. | Styles remain centralized under `src/styles/` but mirror the React domains and use CSS Modules. | Preserves centralized styling while keeping styles easy to locate and locally scoped. |
| Static assets are stored together under the old asset structure. | Assets are grouped under `public/assets/app`, `home`, and `game`. | Makes asset ownership consistent with the domain-based application structure. |

---

## Separation of Responsibilities

Several parts of the existing application already contain responsibilities that can be separated naturally when moved to React.

### Game

The Game feature separates the route-level page from the behavior it uses:

- `GamePage.tsx` coordinates the Game screen.
- `Board.tsx` and `Cell.tsx` handle board presentation.
- `useGamePolling.ts` owns polling behavior.
- `useGameSession.ts` handles React-facing game session behavior.
- `boardService.ts` handles board and move operations.
- `gameSessionService.ts` handles game session operations.
- `scoreboardService.ts` handles score-related operations.
- `gameStore.ts` owns Game-specific shared state.
- `boardLogic.ts` and `gameCode.ts` remain pure utility logic.

This separation reduces the amount of logic that must stay inside one Game page or service file.

### History

Instead of one page handling all history representations, History is separated into:

- `HistoryPage.tsx` as the route container.
- `RoomHistoryView.tsx` for room history.
- `PlayerHistoryView.tsx` for player history.
- `RoundHistoryView.tsx` for round details.
- `HistoryReplay.tsx` for replay behavior.
- `useHistoryData.ts` for loading and view-related state.
- `historyFormatting.ts` for formatting helpers.

The page coordinates these pieces instead of implementing every responsibility itself.

### Home

Home-specific actions remain together under `features/home/`, including create, join, spectate, instructions, waiting-room behavior, and notices. These components are not placed in the global `components/` folder because they belong specifically to the Home domain.

---

## Shared vs. Feature-Specific Code

The distinction between shared and feature-specific code is intentional.

For example, `Button`, `Card`, `Modal`, and `ConfirmModal` can be used by different features, so they belong under `src/components/`.

By contrast, `Board`, `Scoreboard`, and `EmotePicker` only belong to the Game domain, so they remain under `features/game/components/`.

`CopyableCode` is shared because the same behavior can be needed by more than one domain. This avoids duplicating equivalent UI while preventing the shared folder from becoming a place for feature-specific components.

---

## Pages and Routing

Pages are stored inside their owning feature:

```text
features/home/pages/HomePage.tsx
features/game/pages/GamePage.tsx
features/history/pages/HistoryPage.tsx
```

A page represents a navigable route. Components such as result dialogs, quit confirmations, emote selection, and other in-page behavior are kept as components instead of being treated as pages.

`NotFoundPage.tsx` remains under `src/app/` because it belongs to application routing rather than to Home, Game, or History.

---

## Styling Structure

The project keeps CSS separate from component files, but the styles follow the same domain organization as the source code.

For example:

```text
src/features/game/components/Board.tsx
src/styles/features/game/Board.module.css
```

This keeps styling centralized while still making the corresponding stylesheet predictable to locate. CSS Modules provide component-level class scoping without requiring all styles to be physically co-located with the component.

Global concerns such as resets, layout rules, responsive rules, and design tokens stay directly under `src/styles/`.

---

## Naming Conventions

| Type | Convention | Example |
|---|---|---|
| React components | PascalCase | `Board.tsx`, `CreateGameModal.tsx` |
| Pages | PascalCase with `Page` suffix | `GamePage.tsx` |
| Hooks | camelCase beginning with `use` | `useGamePolling.ts` |
| Services | camelCase with descriptive service name | `gameSessionService.ts` |
| API modules | camelCase | `tictactoeApi.ts`, `historyApi.ts` |
| Stores | camelCase with `Store` suffix | `gameStore.ts` |
| Utilities | camelCase | `boardLogic.ts`, `historyFormatting.ts` |
| Type names | PascalCase | `GameSession` |
| CSS Modules | Component name + `.module.css` | `Board.module.css` |

These conventions make the role of a file visible from its name and keep naming consistent across the project.

---

## What Is Preserved from the Existing Application

The migration does not replace every existing idea. Several parts of the JavaScript application already map well to the React architecture:

- Existing `components`, `pages`, `services`, `api`, `config`, `state`, and utility concepts remain useful; they are reorganized according to domain ownership.
- Pure game logic such as board evaluation and game-code helpers remains utility logic rather than being placed inside React components.
- Application constants remain configuration concerns.
- The main functional domains remain **Home**, **Game**, and **History**.

The React structure therefore keeps useful separation already present in the JavaScript project while making feature boundaries more explicit and separating responsibilities that are currently combined.

---

## Summary

The proposed structure is designed around four main goals:

1. **Group code by domain** so Home, Game, and History have clear ownership.
2. **Separate responsibilities** so pages and large service files do not contain unrelated behavior.
3. **Keep shared code intentional** by placing only genuinely reusable code in top-level shared folders.
4. **Use consistent React and TypeScript conventions** for components, hooks, routing, state, APIs, services, types, and styles.

This provides a clear foundation for converting the current JavaScript Tic-Tac-Toe application into a maintainable React TypeScript application without forcing a one-to-one copy of the old project structure.
