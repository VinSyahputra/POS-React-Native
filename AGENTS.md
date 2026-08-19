# ReactNative — Expo App

Single-screen Expo application (React Native 0.86 + React 19 + TypeScript strict) targeting iOS, Android, and web. Currently a "Hello World" starter with no navigation, auth, or backend.

> **Read `README.md` for setup instructions and environment variables before making changes.**
> (No `README.md` exists yet — until one is added, use [docs/agents/workflows.md](docs/agents/workflows.md) for setup, commands, and env-var rules.)

## ⚠️ Expo HAS CHANGED

Read the exact versioned docs at https://docs.expo.dev/versions/v57.0.0/ before writing any code.

## Repository Map

```
.
├── index.ts            # Entry point — registerRootComponent(App)
├── App.tsx             # Root component: SafeAreaProvider + StatusBar + HomeScreen
├── app.json            # Expo config (name, slug, icons, platform settings)
├── assets/             # App icons / adaptive icon layers / favicon
├── src/
│   └── screens/        # Screen components (HomeScreen.tsx)
├── docs/agents/        # Deeper agent documentation (see TOC)
├── tsconfig.json       # extends expo/tsconfig.base, strict: true
└── package.json        # Expo ~57.0.14 scripts: start / android / ios / web
```

## Architecture & Data Flow (high level)

1. `index.ts` calls `registerRootComponent(App)` — works in Expo Go, dev builds, and web.
2. `App.tsx` wraps the tree in `SafeAreaProvider` (react-native-safe-area-context), sets `StatusBar` (expo-status-bar), and renders `HomeScreen`.
3. Screens are default-exported function components in `src/screens/` with `StyleSheet.create` styles.
4. No navigation, state management, API layer, or database yet — plain client-side app.

## Table of Contents

1. [Coding Standards](docs/agents/coding-standards.md) — style rules, how to add a screen or dependency
2. [Project Context](docs/agents/project-context.md) — deep architecture; auth/RBAC/DB status (mostly "not implemented")
3. [Workflows](docs/agents/workflows.md) — real commands, env-var handling, security, task templates
4. [Memory](docs/agents/memory.md) — pitfalls & lessons learned (append-only)
