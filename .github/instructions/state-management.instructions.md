---
applyTo: "**/*.dart"
---

# State Management with Provider

## 🎯 Provider Basics

Provider is Flutter's recommended state management solution for most apps. It's simple, scalable, and well-documented.

## 📋 Provider Types

| Provider Type | Use Case |
|--------------|----------|
| `Provider` | Expose a value (read-only) |
| `ChangeNotifierProvider` | Mutable state that notifies listeners |
| `FutureProvider` | Async data that loads once |
| `StreamProvider` | Reactive stream data |

## 🏗️ ChangeNotifier Pattern (Primary)

### Creating a Provider

```dart
// lib/src/features/counter/providers/counter_provider.dart
import 'package:flutter/foundation.dart';

class CounterProvider extends ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }

  void decrement() {
    _count--;
    notifyListeners();
  }

  void reset() {
    _count = 0;
    notifyListeners();
  }
}
```

### More Complete Example

```dart
// lib/src/features/todos/providers/todo_provider.dart
import 'package:flutter/foundation.dart';
import '../models/todo.dart';

class TodoProvider extends ChangeNotifier {
  final List<Todo> _todos = [];
  bool _isLoading = false;
  String? _error;

  // Getters
  List<Todo> get todos => List.unmodifiable(_todos);
  bool get isLoading => _isLoading;
  String? get error => _error;
  int get completedCount => _todos.where((t) => t.isCompleted).length;

  // Actions
  void addTodo(String title) {
    _todos.add(Todo(
      id: DateTime.now().millisecondsSinceEpoch.toString(),
      title: title,
    ));
    notifyListeners();
  }

  void toggleTodo(String id) {
    final index = _todos.indexWhere((t) => t.id == id);
    if (index != -1) {
      _todos[index] = _todos[index].copyWith(
        isCompleted: !_todos[index].isCompleted,
      );
      notifyListeners();
    }
  }

  void removeTodo(String id) {
    _todos.removeWhere((t) => t.id == id);
    notifyListeners();
  }

  Future<void> loadTodos() async {
    _isLoading = true;
    _error = null;
    notifyListeners();

    try {
      // Simulate API call
      await Future.delayed(const Duration(seconds: 1));
      // _todos.addAll(fetchedTodos);
    } catch (e) {
      _error = e.toString();
    } finally {
      _isLoading = false;
      notifyListeners();
    }
  }
}
```

## 📱 Registering Providers

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
        ChangeNotifierProvider(create: (_) => CounterProvider()),
        ChangeNotifierProvider(create: (_) => TodoProvider()),
        ChangeNotifierProvider(create: (_) => AuthProvider()),
      ],
      child: MaterialApp(
        title: 'My App',
        home: const HomeScreen(),
      ),
    );
  }
}
```

## 🔧 Consuming Providers

### Method 1: context.watch (Rebuilds on change)

```dart
class CounterDisplay extends StatelessWidget {
  const CounterDisplay({super.key});

  @override
  Widget build(BuildContext context) {
    // Rebuilds when count changes
    final count = context.watch<CounterProvider>().count;

    return Text('Count: $count');
  }
}
```

### Method 2: context.read (No rebuild, for actions)

```dart
class IncrementButton extends StatelessWidget {
  const IncrementButton({super.key});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      // Use read for actions - doesn't rebuild widget
      onPressed: () => context.read<CounterProvider>().increment(),
      child: const Text('Increment'),
    );
  }
}
```

### Method 3: Consumer (Granular rebuilds)

```dart
class TodoScreen extends StatelessWidget {
  const TodoScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Todos')),
      body: Consumer<TodoProvider>(
        builder: (context, todoProvider, child) {
          if (todoProvider.isLoading) {
            return const Center(child: CircularProgressIndicator());
          }

          if (todoProvider.error != null) {
            return Center(child: Text('Error: ${todoProvider.error}'));
          }

          return ListView.builder(
            itemCount: todoProvider.todos.length,
            itemBuilder: (context, index) {
              final todo = todoProvider.todos[index];
              return TodoTile(todo: todo);
            },
          );
        },
      ),
    );
  }
}
```

### Method 4: Selector (Select specific properties)

```dart
class TodoCount extends StatelessWidget {
  const TodoCount({super.key});

  @override
  Widget build(BuildContext context) {
    // Only rebuilds when completedCount changes
    final completed = context.select<TodoProvider, int>(
      (provider) => provider.completedCount,
    );

    return Text('Completed: $completed');
  }
}
```

## 📋 Provider Rules

### ✅ Do's

- Use `context.read` in callbacks and event handlers
- Use `context.watch` or `Consumer` for reactive UI
- Keep providers focused on single responsibility
- Use `notifyListeners()` after state changes
- Make lists unmodifiable with getters

### ❌ Don'ts

- Don't use `context.watch` in callbacks (causes rebuilds)
- Don't call `notifyListeners()` in constructor
- Don't store BuildContext in providers
- Don't put UI logic in providers

## 🎯 State Management Decision Guide

```dart
// Reading state that should trigger rebuilds
final value = context.watch<MyProvider>().someValue;

// Reading state in event handlers (no rebuild)
onPressed: () {
  context.read<MyProvider>().doSomething();
}

// Reading state once in initState
@override
void initState() {
  super.initState();
  context.read<MyProvider>().loadData();
}
```

## 🔄 Async Operations

```dart
class DataProvider extends ChangeNotifier {
  List<Item> _items = [];
  bool _isLoading = false;
  String? _errorMessage;

  // State getters
  List<Item> get items => _items;
  bool get isLoading => _isLoading;
  String? get errorMessage => _errorMessage;
  bool get hasError => _errorMessage != null;

  Future<void> fetchItems() async {
    _isLoading = true;
    _errorMessage = null;
    notifyListeners();

    try {
      // Your API call here
      await Future.delayed(const Duration(seconds: 1));
      _items = [/* fetched data */];
    } catch (e) {
      _errorMessage = 'Failed to load items: $e';
    } finally {
      _isLoading = false;
      notifyListeners();
    }
  }
}
```

This pattern provides clean separation between UI and business logic while keeping things simple and maintainable.
