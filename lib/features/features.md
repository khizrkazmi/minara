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
