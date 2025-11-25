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
