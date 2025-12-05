---
applyTo: "**/*.dart"
---

# Flutter Project Architecture

## 📁 Project Structure

```
lib/
├── main.dart                    # App entry point
└── src/
    ├── core/                    # Core infrastructure
    │   ├── theme/               # Design system
    │   │   ├── app_theme.dart
    │   │   ├── color_palette.dart
    │   │   └── text_styles.dart
    │   └── navigation/          # Routing (if needed)
    │       └── routes.dart
    ├── features/                # Business features
    │   └── [feature_name]/      # Feature folder
    │       ├── models/          # Data models
    │       │   └── [model].dart
    │       ├── providers/       # State management
    │       │   └── [feature]_provider.dart
    │       ├── screens/         # Full page widgets
    │       │   └── [feature]_screen.dart
    │       └── widgets/         # Feature-specific widgets
    │           └── [widget].dart
    └── shared/                  # Shared utilities
        ├── widgets/             # Reusable UI components
        │   └── [component].dart
        ├── constants/           # App constants
        │   └── constants.dart
        └── extensions/          # Dart extensions
            └── extensions.dart
```

## 🏗️ Architecture Layers

### **Core Layer**
- **Purpose**: App foundation - theme, navigation, configuration
- **Dependencies**: None (foundation layer)
- **Examples**: Theme data, color palette, text styles, route definitions

### **Features Layer**
- **Purpose**: Business logic and UI for specific features
- **Dependencies**: Core and Shared layers
- **Structure**: Models → Providers → Screens/Widgets

### **Shared Layer**
- **Purpose**: Reusable components across features
- **Dependencies**: Core layer only
- **Examples**: Custom buttons, text fields, loading indicators

## 🔄 Data Flow Pattern

```
User Input → Screen → Provider → Model
                ↑         ↓
              Widget ← State Change
```

## 📋 File Naming Conventions

- **Models**: `user.dart`, `product.dart` (singular, lowercase)
- **Providers**: `auth_provider.dart`, `cart_provider.dart` (snake_case + _provider)
- **Screens**: `home_screen.dart`, `login_screen.dart` (snake_case + _screen)
- **Widgets**: `user_card.dart`, `product_tile.dart` (snake_case, descriptive)

## 🎯 Feature Organization

Each feature should be self-contained:

```
features/
├── auth/
│   ├── models/
│   │   └── user.dart
│   ├── providers/
│   │   └── auth_provider.dart
│   ├── screens/
│   │   ├── login_screen.dart
│   │   └── register_screen.dart
│   └── widgets/
│       └── auth_form.dart
├── home/
│   ├── providers/
│   │   └── home_provider.dart
│   ├── screens/
│   │   └── home_screen.dart
│   └── widgets/
│       ├── feature_card.dart
│       └── stats_widget.dart
```

## 🚀 Getting Started Template

```dart
// main.dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MultiProvider(
      providers: [
        // Register your providers here
        ChangeNotifierProvider(create: (_) => YourProvider()),
      ],
      child: MaterialApp(
        title: 'App Name',
        theme: ThemeData(
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
          useMaterial3: true,
        ),
        home: const HomeScreen(),
      ),
    );
  }
}
```

This architecture ensures clean separation of concerns and scalability for Flutter apps.
