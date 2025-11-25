# File structure for the Figma implementation

This layout keeps design assets, shared UI primitives, and Firebase-powered features organized so screens can be built quickly from consistent building blocks.

## Directory map

```
lib/
├── app/
│   ├── theme/               # Colors, typography, spacing, component theming
│   └── app.dart             # Root MaterialApp wiring the theme + navigation
├── features/                # Feature-first folders (e.g., auth, dashboard, courses)
│   └── <feature_name>/
│       ├── data/            # Firebase services, repositories, models
│       ├── application/     # State management (controllers/notifiers)
│       └── presentation/    # Screens + widgets for this feature
├── shared/                  # Reusable UI atoms/molecules (buttons, cards, inputs)
├── services/                # Cross-cutting services (analytics, remote config)
└── utils/                   # Helpers (formatters, validators, extensions)

assets/
├── icons/                   # Exported SVGs from Figma
├── images/                  # Raster images/PNGs
├── illustrations/           # Hero/empty-state art
└── fonts/                   # Custom font families from Figma
```

## How to use it
- **Icons**: Export SVGs from the Figma icon frame into `assets/icons/` and load them with `flutter_svg`. Keep semantic names (e.g., `ic_home.svg`) and surface them through an `AppIcons` map/class inside `lib/shared/`.
- **Theme**: Define color tokens, text styles, spacing, and component themes in `lib/app/theme/`. Use a single `AppTheme` (in `app.dart`) so every screen and widget reads from the same design system.
- **Widgets**: Place shared buttons/cards/inputs in `lib/shared/` to avoid duplication. Feature-specific widgets live under that feature’s `presentation/` folder.
- **Firebase**: Initialize in `main.dart` (already set up). Put Firestore/Storage/Auth accessors in `features/<feature>/data/`, and expose UI-friendly models via repositories so widgets stay declarative.
- **Navigation**: Add your router (e.g., `GoRouter`, `RouterConfig`) alongside `AppTheme` in `lib/app/app.dart` so features register routes in one place.

This structure keeps the design system centralized while giving each feature its own space for data, state, and UI layers.

## Next steps checklist
1. **Export assets from Figma**
   - Download icons as SVGs into `assets/icons/` and add semantic names (`ic_home.svg`, `ic_search.svg`).
   - Export illustrations/hero art into `assets/illustrations/` and raster images into `assets/images/`.
   - Place custom font files from Figma into `assets/fonts/` and wire them into `pubspec.yaml` under `fonts`.

2. **Install UI dependencies**
   - Add `flutter_svg` for vector icons, and `google_fonts` if you want to pull fonts from the network during development.
   - Run `flutter pub get` after updating `pubspec.yaml`.

3. **Create the design system** (`lib/app/theme/`)
   - Add files for `colors.dart`, `typography.dart`, `spacing.dart`, and `components.dart` (button/input themes).
   - Expose a single `AppTheme.light` (and dark if needed) and apply it in `lib/app/app.dart` when building `MaterialApp`/`MaterialApp.router`.

4. **Set up routing** (`lib/app/app.dart`)
   - Configure your router (e.g., GoRouter) and register routes for each feature screen.
   - Keep route names/paths in one place so navigation stays consistent across the app.

5. **Build shared UI atoms** (`lib/shared/`)
   - Create reusable widgets (buttons, icon buttons, text fields, chips, cards) that read from the design system and accept semantic icon names from `AppIcons`.

6. **Scaffold feature folders** (`lib/features/<feature>/`)
   - `data/`: repositories/services that call Firebase (Firestore, Auth, Storage) and map responses to models.
   - `application/`: state management (e.g., Riverpod notifiers, ChangeNotifiers, Cubits) that orchestrate data and UI events.
   - `presentation/`: screens and widgets that render UI and call into the application layer.

7. **Connect Firebase data to UI**
   - Keep Firebase imports inside the `data/` layer; expose typed models and methods for the application layer.
   - In widgets, listen to state providers/notifiers that consume repositories—avoid direct Firebase calls from UI code.

8. **Smoke-test the shell**
   - Run `flutter pub get` and `flutter analyze` to verify the scaffold compiles.
   - Launch the app to confirm the theme and router load before layering in feature screens.
