# 🚀 The Future-Ready Flutter Engineer

## AI-Powered Flutter Development Workshop

**DevFest Akure 2025** | Workshop Template

> *"Flutter is evolving fast — but AI is evolving faster. Developers who learn to combine both aren't just keeping up… they're pulling ahead."*

---

## 📋 What This Is

This is a **starter template** for AI-assisted Flutter development. Fork this repository and use it as your base for vibe coding with AI tools like GitHub Copilot.

The project includes **Copilot Instructions** (`.github/instructions/`) that guide AI assistants to generate Flutter code following best practices.

---

## 🛠️ Prerequisites

Before the workshop, make sure you have:

- [ ] [Flutter SDK](https://docs.flutter.dev/get-started/install) installed
- [ ] [VS Code](https://code.visualstudio.com/) with Flutter extension
- [ ] [GitHub Copilot](https://github.com/features/copilot) extension installed
- [ ] A [Supabase](https://supabase.com/) account (free tier is fine)

### 🎓 Student Benefits

If you're a student, you can get **free access** to premium AI tools:

- **GitHub Student Developer Pack**: [education.github.com/pack](https://education.github.com/pack)
  - Free GitHub Copilot
  - Free domain names, cloud credits, and more!

---

## 🚀 Quick Start

### 1. Fork & Clone

```bash
# Fork this repo on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/devfest-akure-workshop.git
cd devfest-akure-workshop
```

### 2. Create Flutter Project

```bash
# Create a new Flutter project in this directory
flutter create . --project-name posts_app

# Get dependencies
flutter pub get
```

### 3. Add Dependencies

Add these to your `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  supabase_flutter: ^2.3.0
  provider: ^6.1.0
```

Then run:

```bash
flutter pub get
```

### 4. Setup Supabase

1. Go to [supabase.com](https://supabase.com) and create a new project
2. Copy your **Project URL** and **Anon Key** from Settings > API
3. **That's it!** We'll use the **Supabase MCP** to create tables and everything else via AI

> 💡 **No SQL required!** The Supabase MCP (Model Context Protocol) allows AI to directly interact with your Supabase project - creating tables, setting up RLS policies, and more.

### 5. Configure Your App

Update `lib/main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:supabase_flutter/supabase_flutter.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();

  await Supabase.initialize(
    url: 'YOUR_SUPABASE_URL',      // Replace with your URL
    anonKey: 'YOUR_SUPABASE_ANON_KEY',  // Replace with your anon key
  );

  runApp(const MyApp());
}

final supabase = Supabase.instance.client;

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Posts App',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const Scaffold(
        body: Center(child: Text('Ready to vibe code! 🚀')),
      ),
    );
  }
}
```

---

## 🤖 Using AI to Build

Now the fun part! Use GitHub Copilot to build your app.

### How Copilot Instructions Work

The `.github/instructions/` folder contains markdown files that guide Copilot on how to write Flutter code. When you prompt Copilot, it will follow these guidelines automatically.

**Included instructions:**
- `main-architecture.instructions.md` - Project structure
- `effective-dart.instructions.md` - Dart style guide
- `state-management.instructions.md` - Provider patterns
- `ui-components.instructions.md` - Widget guidelines
- `widget-anti-patterns.instructions.md` - What NOT to do
- `mobile-ux-patterns.instructions.md` - UX best practices
- `supabase-flutter.instructions.md` - Supabase integration

### Tips for Effective Prompting

1. **Be specific**: "Create a posts list screen that fetches posts from Supabase and displays them in a ListView"

2. **Reference the architecture**: "Following the project structure, create a PostsProvider in the features/posts/providers folder"

3. **Ask for complete features**: "Build a complete create post feature with a form screen, provider method, and Supabase integration"

4. **Iterate**: Start simple, then ask Copilot to enhance

---

## 📁 Project Structure

After vibe coding, your project should look something like:

```
lib/
├── main.dart
└── src/
    ├── core/
    │   └── theme/
    ├── features/
    │   ├── auth/
    │   │   ├── providers/
    │   │   ├── screens/
    │   │   └── widgets/
    │   └── posts/
    │       ├── models/
    │       │   └── post.dart
    │       ├── providers/
    │       │   └── posts_provider.dart
    │       ├── screens/
    │       │   ├── posts_list_screen.dart
    │       │   └── create_post_screen.dart
    │       └── widgets/
    │           └── post_card.dart
    └── shared/
        └── widgets/
```

---

## 🎯 Workshop Goals

By the end of this workshop, you'll have:

- [ ] A working Flutter app connected to Supabase
- [ ] Posts list with pull-to-refresh
- [ ] Create post functionality
- [ ] (Bonus) Edit and delete posts
- [ ] (Bonus) User authentication

---

## 🔗 Resources

- [Flutter Documentation](https://docs.flutter.dev/)
- [Supabase Documentation](https://supabase.com/docs)
- [Provider Package](https://pub.dev/packages/provider)
- [GitHub Copilot Docs](https://docs.github.com/en/copilot)

---

## 🤝 Workshop Speaker

**Fola Oluwafemi**

- 𝕏 Twitter: [@folabuilds](https://x.com/folabuilds)
- LinkedIn: [/in/fola-oluwafemi](https://linkedin.com/in/fola-oluwafemi)

**Workshop**: *"The Future-Ready Flutter Engineer: Mastering AI in Your Workflow"*

DevFest Akure 2025

---

## 📝 License

MIT License - Feel free to use this template for your own learning!
