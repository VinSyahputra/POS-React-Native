# Coding Standards

Grounded in the actual code at the initial commit. Keep new code consistent with what is already here.

## Stack & General Style

- TypeScript with `strict: true` (`tsconfig.json` extends `expo/tsconfig.base`). Avoid `any`; type public component props explicitly.
- Expo SDK ~57 → React Native 0.86, React 19.2.3, react-native-web 0.21, Node ≥ 22.13.
- **Install Expo/native packages with `npx expo install <pkg>`** so versions match the installed SDK — never pick versions by hand.
- Function components only (no class components). One component per file, PascalCase filenames (`HomeScreen.tsx`).
- Named exports for utilities; default export for screen/page components (matches `App.tsx` → `import HomeScreen from './src/screens/HomeScreen'`).

## Screen Component Pattern

Copy the existing pattern from `src/screens/HomeScreen.tsx`:

```tsx
import { StyleSheet, Text, View } from 'react-native';
import { SafeAreaView } from 'react-native-safe-area-context';

export default function MyScreen() {
  return (
    <SafeAreaView style={styles.safeArea} edges={['top', 'bottom']}>
      <View style={styles.container}>
        {/* ... */}
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: { flex: 1, backgroundColor: '#0f172a' },
  container: { flex: 1, alignItems: 'center', justifyContent: 'center', paddingHorizontal: 24 },
});
```

Checklist for every screen:

- [ ] Default-exported function component in `src/screens/`
- [ ] `SafeAreaView` **from `react-native-safe-area-context`** with explicit `edges` — not the React Native core one
- [ ] Single `StyleSheet.create` object at the bottom of the file — no inline objects for static styles
- [ ] Dark theme palette currently in use: bg `#0f172a`, text `#ffffff`, muted `#94a3b8`; keep new colors consistent until a theme module exists *(assumption — no theme system yet)*

## How to Add a Screen

1. Create `src/screens/<Name>Screen.tsx` using the pattern above.
2. There is **no navigator yet** — render the new screen from `App.tsx` (replace or conditionally swap `HomeScreen`).
3. Verify with `npx tsc --noEmit`, then smoke-test via `npx expo start`.

## How to Add a Dependency

```bash
npx expo install <package>   # anything Expo SDK-related or native
npm install <package>        # acceptable for pure-JS utilities only
```

State the reason for the addition in the commit message. Prefer Expo SDK / documented third-party libraries (see the SDK reference at https://docs.expo.dev/versions/v57.0.0/).

## Data Shapes / DTO Conventions

No API layer exists yet. When the first one lands: put request/response types in `src/types/` (one file per domain), PascalCase interfaces, components must not import from type files' internals. *(assumption — revisit when an API client is added)*

## Validation Rules

None implemented (no forms yet). When forms arrive, validate with a schema library at the input boundary before state is updated. *(assumption)*
