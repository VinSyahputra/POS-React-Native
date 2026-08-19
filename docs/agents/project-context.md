# Project Context — Deep Architecture

Early-stage Expo client app. Most server-side concepts do not exist; each is stated explicitly so agents do not hunt for missing layers.

## Entry / Registration Chain

- `index.ts` → `registerRootComponent(App)` (from `expo`) — sets up the component for Expo Go, native builds, and web.
- `App.tsx` → `SafeAreaProvider` → `StatusBar` (`expo-status-bar`, `style="light"`) → `HomeScreen`.
- `src/screens/HomeScreen.tsx` — centered title/subtitle on a dark background inside `SafeAreaView` with `edges={['top','bottom']}`.

## Expo App Config (`app.json`)

- `name`/`slug`: `ReactNative`, version `1.0.0`, portrait orientation, `userInterfaceStyle: "light"`.
- iOS: tablet support enabled. Android: adaptive icon (foreground/background/monochrome layers from `assets/`), predictive back gesture disabled.
- Web: favicon from `assets/`. No config plugins, no EAS build config, no `app.config.js`.

## Platform Targets

iOS, Android, and Web (`react-native-web` installed; `npm run web`). Safe-area handling via `react-native-safe-area-context` across all platforms. `ios/` and `android/` native folders are not checked in — this is a managed/prebuild-style project.

## Authentication Flow

**Not implemented.** No login screen, token storage, or session logic anywhere in `src/`. If added later, the natural places are `src/screens/LoginScreen.tsx`, `expo-secure-store` for tokens, and an auth gate in `App.tsx`. *(assumption — nothing exists in code today)*

## RBAC Design & Permission Flow

**Not applicable — no roles or permissions.** Single-audience client app with no backend.

## Database & Query Patterns

**None.** No SQLite/AsyncStorage/WatermelonDB and no remote API. All state is component-local `useState`.

## Middleware Strategy & Ordering

**Not applicable — client app, not a server.** Closest analogues: providers mounted in `App.tsx` (currently only `SafeAreaProvider`) and future navigation state.

## State Management

Component-local state only. No Redux/Zustand/Context providers. Re-evaluate once two or more screens share state.

## Navigation

**None installed** (no expo-router, no react-navigation). `App.tsx` renders `HomeScreen` directly. Adding navigation is the first structural change this app is likely to need.
