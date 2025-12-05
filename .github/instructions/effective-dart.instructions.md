---
applyTo: "**/*.dart"
---

# Effective Dart Rules

## 🎯 Naming Conventions

### Types & Classes
- `UpperCamelCase` for classes, enums, typedefs, type parameters
- `UpperCamelCase` for extensions
- Capitalize acronyms > 2 letters like words (`HttpClient`, not `HTTPClient`)

### Variables & Functions
- `lowerCamelCase` for variables, parameters, functions
- `lowercase_with_underscores` for packages, directories, files, import prefixes
- Avoid abbreviations unless more common than full term

### Naming Patterns
```dart
// Good naming examples
class UserService {}           // Class
enum ConnectionStatus {}       // Enum
String userName = '';          // Variable
void loadUserData() {}         // Function
bool isLoggedIn = false;       // Boolean (positive form)
```

## 🏗️ Code Structure

### Type Annotations
```dart
// Required annotations
String? name;                  // Variables without initializers
final List<User> users = [];   // When type isn't obvious
User getUser(String id) {}     // Function return types
void login(String email) {}    // Parameter types
```

### Constructors & Functions
```dart
// Constructor patterns
class User {
  final String name;
  final int age;

  const User({required this.name, required this.age});  // Const constructor
  User.guest() : name = 'Guest', age = 0;              // Named constructor
}

// Function patterns
Future<void> fetchData() async {}      // Async functions return Future<void>
String get fullName => '$first $last'; // Getters for computed properties
```

## 📦 Imports & Organization

```dart
// Import order (separate with blank lines)
import 'dart:core';                     // 1. Dart SDK
import 'dart:async';

import 'package:flutter/material.dart'; // 2. Flutter framework
import 'package:provider/provider.dart';// 3. Third-party packages

import '../core/theme.dart';            // 4. Relative imports (project files)
import 'widgets/my_widget.dart';
```

## 🎨 Code Style

### Control Flow
```dart
// Keep simple statements on one line when possible
if (condition) doSomething();

// Prefer guard clauses for early exits
if (invalid) return;  // Instead of wrapping main logic in if blocks

// Prefer final over var
final String name = 'John';
const int maxRetries = 3;
```

### Collections
```dart
// Use collection literals
final List<String> names = [];        // Not List<String>()
final Map<String, int> scores = {};   // Not Map<String, int>()

// Use collection methods
final adults = users.where((user) => user.age >= 18);
final names = users.map((user) => user.name);
```

### Null Safety
```dart
// Use null-aware operators
final name = user?.name ?? 'Unknown';
final length = list?.length ?? 0;

// Use late for lazy initialization
late final String computedValue;
```

### Error Handling
```dart
// Use specific catch blocks
try {
  await riskyOperation();
} on FormatException catch (e) {
  print('Format error: $e');
} on HttpException catch (e) {
  print('Network error: $e');
} catch (e) {
  print('Unknown error: $e');
  rethrow;  // Preserve stack trace when re-throwing
}
```

## ✅ Best Practices Summary

| Do | Don't |
|-----|-------|
| Use `const` constructors | Create mutable objects unnecessarily |
| Prefer `final` for variables | Use `var` when value won't change |
| Use named parameters for clarity | Use positional params for many args |
| Keep functions small and focused | Write long functions with many tasks |
| Use meaningful names | Use abbreviations like `btn`, `txt` |
| Document public APIs | Leave public APIs undocumented |
