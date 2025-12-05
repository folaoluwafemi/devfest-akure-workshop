---
applyTo: "**/*.dart"
---

# Widget Anti-Patterns

## 🚫 NEVER: Widget Methods/Functions

**Do NOT create methods that return widgets.** Always use dedicated widget classes.

### ❌ BAD - Widget Methods

```dart
class MyScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        _buildHeader(),      // ❌ WRONG
        _buildContent(),     // ❌ WRONG
        _buildFooter(),      // ❌ WRONG
      ],
    );
  }

  // ❌ NEVER DO THIS
  Widget _buildHeader() {
    return Container(
      child: Text('Header'),
    );
  }

  // ❌ NEVER DO THIS
  Widget _buildContent() {
    return ListView.builder(
      itemCount: 10,
      itemBuilder: (context, index) => ListTile(title: Text('Item $index')),
    );
  }

  // ❌ NEVER DO THIS
  Widget _buildFooter() {
    return Text('Footer');
  }
}
```

### ✅ GOOD - Dedicated Widget Classes

```dart
class MyScreen extends StatelessWidget {
  const MyScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return const Column(
      children: [
        HeaderWidget(),      // ✅ CORRECT
        ContentWidget(),     // ✅ CORRECT
        FooterWidget(),      // ✅ CORRECT
      ],
    );
  }
}

// ✅ ALWAYS DO THIS
class HeaderWidget extends StatelessWidget {
  const HeaderWidget({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
      child: const Text('Header'),
    );
  }
}

// ✅ ALWAYS DO THIS
class ContentWidget extends StatelessWidget {
  const ContentWidget({super.key});

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: 10,
      itemBuilder: (context, index) => ListTile(title: Text('Item $index')),
    );
  }
}

// ✅ ALWAYS DO THIS
class FooterWidget extends StatelessWidget {
  const FooterWidget({super.key});

  @override
  Widget build(BuildContext context) {
    return const Text('Footer');
  }
}
```

## 🤔 Why Does This Matter?

### 1. **Performance**
Widget methods don't get optimized by Flutter's widget tree. Dedicated widgets can be `const` and skip unnecessary rebuilds.

### 2. **Testability**
You can't easily test `_buildHeader()` in isolation. You can easily test `HeaderWidget()`.

### 3. **Reusability**
Widget methods are tied to their parent class. Dedicated widgets can be used anywhere.

### 4. **Hot Reload**
Widget classes work better with Flutter's hot reload feature.

### 5. **Readability**
Clear widget boundaries make code easier to understand and maintain.

## 📋 Quick Reference

| Pattern | Status | Example |
|---------|--------|---------|
| Widget methods | ❌ BAD | `Widget _buildHeader() => ...` |
| Widget functions | ❌ BAD | `Widget buildHeader() => ...` |
| StatelessWidget class | ✅ GOOD | `class HeaderWidget extends StatelessWidget` |
| StatefulWidget class | ✅ GOOD | `class HeaderWidget extends StatefulWidget` |

## 🔄 Refactoring Example

### Before (Anti-pattern)

```dart
class ProfileScreen extends StatelessWidget {
  Widget _buildAvatar(String url) {
    return CircleAvatar(backgroundImage: NetworkImage(url));
  }

  Widget _buildStats(int followers, int following) {
    return Row(
      children: [
        Text('$followers followers'),
        Text('$following following'),
      ],
    );
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        _buildAvatar('url'),
        _buildStats(100, 50),
      ],
    );
  }
}
```

### After (Correct Pattern)

```dart
class ProfileScreen extends StatelessWidget {
  const ProfileScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return const Column(
      children: [
        ProfileAvatar(url: 'url'),
        ProfileStats(followers: 100, following: 50),
      ],
    );
  }
}

class ProfileAvatar extends StatelessWidget {
  final String url;

  const ProfileAvatar({super.key, required this.url});

  @override
  Widget build(BuildContext context) {
    return CircleAvatar(backgroundImage: NetworkImage(url));
  }
}

class ProfileStats extends StatelessWidget {
  final int followers;
  final int following;

  const ProfileStats({
    super.key,
    required this.followers,
    required this.following,
  });

  @override
  Widget build(BuildContext context) {
    return Row(
      children: [
        Text('$followers followers'),
        Text('$following following'),
      ],
    );
  }
}
```

## ⚡ Remember

> **Every UI element that could be reused or tested should be its own Widget class.**

This ensures maintainability, testability, and a clean widget tree.
