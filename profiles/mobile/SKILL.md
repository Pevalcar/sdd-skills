---
name: profile-mobile
description: "Reglas específicas para desarrollo móvil (Flutter, React Native, Swift, Kotlin)"
---

# Perfil: Mobile Development

Reglas específicas para aplicaciones móviles nativas y cross-platform.

## Cuándo Cargar

| Indicadores | Acciona este perfil |
|-------------|---------------------|
| `pubspec.yaml` presente | Flutter/Dart |
| `Podfile`, `.xcodeproj` | iOS/Swift |
| `build.gradle`, `AndroidManifest.xml` | Android/Kotlin/Java |
| `package.json` con react-native | React Native |
| `capacitor.config.*` | Capacitor |
| `ionic.config.*` | Ionic |

## Reglas Core

### Lifecycle Management
- Handle app pause/resume explicitly
- Clean up resources on destroy
- Save/load state appropriately
- Background task limitations respected

### Memory Management
- No memory leaks (dangling listeners, timers)
- Image caching策略 implemented
- Large lists use virtualization/pagination
- Dispose patterns followed strictly

### Platform Differences
- Feature parity across supported platforms
- Platform-specific UI when appropriate
- Consistent behavior across devices
- OS version compatibility defined

## Patterns Obligatorios

### State Management
```dart
// Flutter example: BLoC/Cubit pattern
class CounterCubit extends Cubit<int> {
  CounterCubit() : super(0);
  
  void increment() => emit(state + 1);
  void decrement() => emit(state - 1);
}
```

### Navigation
- Deep linking support
- Back button handling
- Transition animations consistent
- Route parameters typed

### Offline Support
- Cache strategy defined (memory, disk, both)
- Sync conflict resolution documented
- Queue operations for network failures
- Last-known-good-state fallback

## Platform-Specific Rules

### iOS/Swift
- Follow Human Interface Guidelines
- Swift concurrency (async/await) preferred over GCD
- Size classes for responsiveness
- Dynamic type for accessibility

### Android/Kotlin
- Material Design 3 guidelines
- Coroutines for async operations
- Jetpack Compose for new UI
- ViewModels for state preservation

### Flutter/Dart
- Widgets should be pure functions where possible
- Use const constructors for static widgets
- Leverage state management solutions (Riverpod, Bloc, Provider)
- Follow Dart style guide

### React Native
- Hermes enabled for production builds
- Flipper for debugging disabled in production
- Bridge traffic monitored
- Native modules minimized

## Commands Comunes

| Platform | Command | Purpose |
|----------|---------|---------|
| Flutter | `flutter analyze` | Static analysis |
| Flutter | `flutter test` | Unit/widget tests |
| Flutter | `flutter build apk` | Android build |
| Flutter | `flutter build ios` | iOS build |
| iOS | `xcodebuild test -scheme MyApp` | Run tests |
| Android | `./gradlew test` | Run tests |
| Android | `./gradlew assembleDebug` | Debug build |

## Anti-Patterns Específicos

| Anti-pattern | Problema | Solución |
|-------------|----------|----------|
| No handling app lifecycle | Data loss, background crashes | Implement didFinishLaunching, applicationWillEnterForeground |
| Holding large objects in state | Memory pressure, OOM kills | Pagination, lazy loading, object pooling |
| Blocking main thread | Jank, ANR crashes | Async operations, workers |
| Ignoring dark mode | Poor UX, accessibility issues | Theme-aware colors, dynamic colors |
| Hardcoded strings | i18n impossible later | Localization from day one |
| No error boundaries | App crash on widget error | Error boundary wrappers |

## Performance Targets

| Metric | Target | Measurement |
|--------|--------|-------------|
| Cold start | < 2 seconds | Time to first paint |
| Hot restart | < 300ms | Time to interactive |
| FPS | 60fps maintained | Frame time < 16ms |
| Memory | < 200MB typical | Profile in Xcode/Android Studio |
| Battery impact | Minimal | Energy profiler |

## Verification Checklist

- [ ] Lifecycle methods implemented correctly
- [ ] No memory leaks detected (profile in Xcode/Android Studio)
- [ ] Works on minimum supported OS version
- [ ] Dark mode supported
- [ ] Landscape/portrait handled if required
- [ ] Network offline scenarios tested
- [ ] Push notifications registered
- [ ] App store guidelines followed
- [ ] Performance within targets
- [ ] Accessibility features present
