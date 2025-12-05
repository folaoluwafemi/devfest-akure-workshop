---
applyTo: "**/*.dart"
---

# Mobile UX Patterns

## 🎯 Core Interaction Patterns

### Touch Gestures
- **Tap**: Primary action, navigation
- **Long Press**: Context menus, additional options
- **Swipe**: Navigate, dismiss, quick actions
- **Pull to Refresh**: Update content lists
- **Pinch to Zoom**: Image/content scaling

### Loading States

```dart
class ContentScreen extends StatelessWidget {
  const ContentScreen({super.key});

  @override
  Widget build(BuildContext context) {
    final provider = context.watch<DataProvider>();

    if (provider.isLoading) {
      return const Center(child: CircularProgressIndicator());
    }

    if (provider.hasError) {
      return ErrorWidget(
        message: provider.errorMessage!,
        onRetry: () => provider.loadData(),
      );
    }

    if (provider.items.isEmpty) {
      return const EmptyState(
        icon: Icons.inbox,
        title: 'No items yet',
        message: 'Add your first item to get started',
      );
    }

    return ItemList(items: provider.items);
  }
}
```

## 📱 Navigation Patterns

### Bottom Navigation
- Use 3-5 primary sections maximum
- Always visible for main app functions
- Use icons WITH labels for clarity

```dart
class MainScreen extends StatefulWidget {
  const MainScreen({super.key});

  @override
  State<MainScreen> createState() => _MainScreenState();
}

class _MainScreenState extends State<MainScreen> {
  int _currentIndex = 0;

  final _screens = const [
    HomeScreen(),
    SearchScreen(),
    ProfileScreen(),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: _screens[_currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        onTap: (index) => setState(() => _currentIndex = index),
        items: const [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
          BottomNavigationBarItem(icon: Icon(Icons.search), label: 'Search'),
          BottomNavigationBarItem(icon: Icon(Icons.person), label: 'Profile'),
        ],
      ),
    );
  }
}
```

### Modal Presentations
- **Bottom sheets**: Secondary actions, filters
- **Full-screen modals**: Complex tasks, forms
- **Dialogs**: Confirmations, alerts

```dart
// Bottom Sheet
void showFilterSheet(BuildContext context) {
  showModalBottomSheet(
    context: context,
    builder: (context) => const FilterSheet(),
  );
}

// Full-screen modal
void showCreateForm(BuildContext context) {
  Navigator.of(context).push(
    MaterialPageRoute(
      fullscreenDialog: true,
      builder: (context) => const CreateFormScreen(),
    ),
  );
}
```

## 🎨 Visual Feedback

### Button States

```dart
class InteractiveButton extends StatefulWidget {
  final VoidCallback onPressed;
  final Widget child;

  const InteractiveButton({
    super.key,
    required this.onPressed,
    required this.child,
  });

  @override
  State<InteractiveButton> createState() => _InteractiveButtonState();
}

class _InteractiveButtonState extends State<InteractiveButton> {
  bool _isPressed = false;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTapDown: (_) => setState(() => _isPressed = true),
      onTapUp: (_) => setState(() => _isPressed = false),
      onTapCancel: () => setState(() => _isPressed = false),
      onTap: widget.onPressed,
      child: AnimatedScale(
        scale: _isPressed ? 0.95 : 1.0,
        duration: const Duration(milliseconds: 100),
        child: widget.child,
      ),
    );
  }
}
```

### Toast Messages

```dart
void showSuccessToast(BuildContext context, String message) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(
      content: Text(message),
      backgroundColor: Colors.green,
      behavior: SnackBarBehavior.floating,
      duration: const Duration(seconds: 2),
    ),
  );
}

void showErrorToast(BuildContext context, String message) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(
      content: Text(message),
      backgroundColor: Colors.red,
      behavior: SnackBarBehavior.floating,
      action: SnackBarAction(
        label: 'Dismiss',
        textColor: Colors.white,
        onPressed: () {},
      ),
    ),
  );
}
```

## 📋 List Patterns

### Pull to Refresh

```dart
class RefreshableList extends StatelessWidget {
  const RefreshableList({super.key});

  @override
  Widget build(BuildContext context) {
    final provider = context.watch<ItemProvider>();

    return RefreshIndicator(
      onRefresh: () => provider.refresh(),
      child: ListView.builder(
        itemCount: provider.items.length,
        itemBuilder: (context, index) {
          return ItemTile(item: provider.items[index]);
        },
      ),
    );
  }
}
```

### Infinite Scroll

```dart
class InfiniteList extends StatelessWidget {
  const InfiniteList({super.key});

  @override
  Widget build(BuildContext context) {
    final provider = context.watch<ItemProvider>();

    return NotificationListener<ScrollNotification>(
      onNotification: (notification) {
        if (notification is ScrollEndNotification) {
          if (notification.metrics.extentAfter < 200) {
            provider.loadMore();
          }
        }
        return false;
      },
      child: ListView.builder(
        itemCount: provider.items.length + (provider.hasMore ? 1 : 0),
        itemBuilder: (context, index) {
          if (index == provider.items.length) {
            return const Center(child: CircularProgressIndicator());
          }
          return ItemTile(item: provider.items[index]);
        },
      ),
    );
  }
}
```

## 🎯 Form Best Practices

### Input Validation

```dart
class LoginForm extends StatefulWidget {
  const LoginForm({super.key});

  @override
  State<LoginForm> createState() => _LoginFormState();
}

class _LoginFormState extends State<LoginForm> {
  final _formKey = GlobalKey<FormState>();
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();

  @override
  void dispose() {
    _emailController.dispose();
    _passwordController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          TextFormField(
            controller: _emailController,
            keyboardType: TextInputType.emailAddress,
            textInputAction: TextInputAction.next,
            decoration: const InputDecoration(labelText: 'Email'),
            validator: (value) {
              if (value == null || value.isEmpty) {
                return 'Please enter your email';
              }
              if (!value.contains('@')) {
                return 'Please enter a valid email';
              }
              return null;
            },
          ),
          const SizedBox(height: 16),
          TextFormField(
            controller: _passwordController,
            obscureText: true,
            textInputAction: TextInputAction.done,
            decoration: const InputDecoration(labelText: 'Password'),
            validator: (value) {
              if (value == null || value.isEmpty) {
                return 'Please enter your password';
              }
              if (value.length < 6) {
                return 'Password must be at least 6 characters';
              }
              return null;
            },
          ),
          const SizedBox(height: 24),
          ElevatedButton(
            onPressed: _submit,
            child: const Text('Login'),
          ),
        ],
      ),
    );
  }

  void _submit() {
    if (_formKey.currentState!.validate()) {
      // Form is valid, proceed with login
      context.read<AuthProvider>().login(
            email: _emailController.text,
            password: _passwordController.text,
          );
    }
  }
}
```

## 📱 Responsive Design

```dart
class ResponsiveLayout extends StatelessWidget {
  final Widget mobile;
  final Widget? tablet;
  final Widget? desktop;

  const ResponsiveLayout({
    super.key,
    required this.mobile,
    this.tablet,
    this.desktop,
  });

  @override
  Widget build(BuildContext context) {
    final width = MediaQuery.of(context).size.width;

    if (width >= 1024 && desktop != null) {
      return desktop!;
    }
    if (width >= 600 && tablet != null) {
      return tablet!;
    }
    return mobile;
  }
}
```

## ✅ UX Checklist

- [ ] Loading states for all async operations
- [ ] Error states with retry option
- [ ] Empty states with helpful guidance
- [ ] Pull to refresh on lists
- [ ] Proper keyboard handling in forms
- [ ] Visual feedback on interactive elements
- [ ] Safe area handling for notches
- [ ] Responsive layouts for different screen sizes
