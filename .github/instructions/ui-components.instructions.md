---
applyTo: "**/*.dart"
---

# UI Components Guide

## 📁 Component Organization

```
lib/src/
├── shared/
│   └── widgets/              # Global reusable components
│       ├── buttons/
│       │   └── app_button.dart
│       ├── inputs/
│       │   └── app_text_field.dart
│       └── cards/
│           └── info_card.dart
└── features/
    └── [feature]/
        └── widgets/          # Feature-specific components
            └── [widget].dart
```

## 🎨 Core Component Patterns

### Button Component

```dart
class AppButton extends StatelessWidget {
  final VoidCallback? onPressed;
  final String text;
  final bool isLoading;
  final bool isOutlined;

  const AppButton({
    super.key,
    required this.onPressed,
    required this.text,
    this.isLoading = false,
    this.isOutlined = false,
  });

  // Named constructors for variants
  const AppButton.outlined({
    super.key,
    required this.onPressed,
    required this.text,
    this.isLoading = false,
  }) : isOutlined = true;

  @override
  Widget build(BuildContext context) {
    final child = isLoading
        ? const SizedBox(
            height: 20,
            width: 20,
            child: CircularProgressIndicator(strokeWidth: 2),
          )
        : Text(text);

    if (isOutlined) {
      return OutlinedButton(
        onPressed: isLoading ? null : onPressed,
        child: child,
      );
    }

    return ElevatedButton(
      onPressed: isLoading ? null : onPressed,
      child: child,
    );
  }
}
```

### Text Field Component

```dart
class AppTextField extends StatelessWidget {
  final String? label;
  final String? hint;
  final TextEditingController? controller;
  final String? Function(String?)? validator;
  final bool obscureText;
  final TextInputType? keyboardType;
  final Widget? prefixIcon;
  final Widget? suffixIcon;

  const AppTextField({
    super.key,
    this.label,
    this.hint,
    this.controller,
    this.validator,
    this.obscureText = false,
    this.keyboardType,
    this.prefixIcon,
    this.suffixIcon,
  });

  @override
  Widget build(BuildContext context) {
    return TextFormField(
      controller: controller,
      validator: validator,
      obscureText: obscureText,
      keyboardType: keyboardType,
      decoration: InputDecoration(
        labelText: label,
        hintText: hint,
        prefixIcon: prefixIcon,
        suffixIcon: suffixIcon,
        border: OutlineInputBorder(
          borderRadius: BorderRadius.circular(8),
        ),
      ),
    );
  }
}
```

### Card Component

```dart
class InfoCard extends StatelessWidget {
  final String title;
  final String? subtitle;
  final Widget? leading;
  final Widget? trailing;
  final VoidCallback? onTap;

  const InfoCard({
    super.key,
    required this.title,
    this.subtitle,
    this.leading,
    this.trailing,
    this.onTap,
  });

  @override
  Widget build(BuildContext context) {
    return Card(
      child: InkWell(
        onTap: onTap,
        borderRadius: BorderRadius.circular(12),
        child: Padding(
          padding: const EdgeInsets.all(16),
          child: Row(
            children: [
              if (leading != null) ...[
                leading!,
                const SizedBox(width: 16),
              ],
              Expanded(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      title,
                      style: Theme.of(context).textTheme.titleMedium,
                    ),
                    if (subtitle != null) ...[
                      const SizedBox(height: 4),
                      Text(
                        subtitle!,
                        style: Theme.of(context).textTheme.bodySmall,
                      ),
                    ],
                  ],
                ),
              ),
              if (trailing != null) trailing!,
            ],
          ),
        ),
      ),
    );
  }
}
```

### Loading Indicator

```dart
class LoadingOverlay extends StatelessWidget {
  final bool isLoading;
  final Widget child;

  const LoadingOverlay({
    super.key,
    required this.isLoading,
    required this.child,
  });

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        child,
        if (isLoading)
          Container(
            color: Colors.black.withOpacity(0.3),
            child: const Center(
              child: CircularProgressIndicator(),
            ),
          ),
      ],
    );
  }
}
```

### Empty State Widget

```dart
class EmptyState extends StatelessWidget {
  final IconData icon;
  final String title;
  final String? message;
  final String? actionLabel;
  final VoidCallback? onAction;

  const EmptyState({
    super.key,
    required this.icon,
    required this.title,
    this.message,
    this.actionLabel,
    this.onAction,
  });

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Padding(
        padding: const EdgeInsets.all(32),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(icon, size: 64, color: Colors.grey),
            const SizedBox(height: 16),
            Text(
              title,
              style: Theme.of(context).textTheme.titleLarge,
              textAlign: TextAlign.center,
            ),
            if (message != null) ...[
              const SizedBox(height: 8),
              Text(
                message!,
                style: Theme.of(context).textTheme.bodyMedium?.copyWith(
                      color: Colors.grey,
                    ),
                textAlign: TextAlign.center,
              ),
            ],
            if (actionLabel != null && onAction != null) ...[
              const SizedBox(height: 24),
              ElevatedButton(
                onPressed: onAction,
                child: Text(actionLabel!),
              ),
            ],
          ],
        ),
      ),
    );
  }
}
```

## 📋 Component Rules

### Structure Requirements

- **Required parameters first**, optional parameters last
- Use **named constructors** for variants (`AppButton.outlined()`)
- Always include **super.key** parameter
- Implement **const constructors** where possible

### Property Organization

```dart
class ComponentName extends StatelessWidget {
  // 1. Required properties first
  final String requiredProperty;
  
  // 2. Optional properties
  final String? optionalProperty;
  
  // 3. Properties with defaults
  final bool isEnabled;

  const ComponentName({
    super.key,
    required this.requiredProperty,
    this.optionalProperty,
    this.isEnabled = true,
  });
}
```

### Theme Integration

```dart
// Use Theme for consistent styling
@override
Widget build(BuildContext context) {
  final theme = Theme.of(context);
  
  return Text(
    'Hello',
    style: theme.textTheme.headlineMedium?.copyWith(
      color: theme.colorScheme.primary,
    ),
  );
}
```

## ✅ Best Practices

| Do | Don't |
|----|-------|
| Use `const` constructors | Create widgets without `const` |
| Extract reusable widgets to classes | Use methods returning widgets |
| Use Theme for colors/styles | Hardcode colors |
| Use named parameters | Use many positional parameters |
| Document public widgets | Leave widgets undocumented |
| Keep widgets small and focused | Create god widgets |

## 🎯 Responsive Sizing

```dart
// Use MediaQuery for responsive layouts
@override
Widget build(BuildContext context) {
  final screenWidth = MediaQuery.of(context).size.width;
  final isTablet = screenWidth > 600;
  
  return Padding(
    padding: EdgeInsets.all(isTablet ? 32 : 16),
    child: isTablet 
        ? TwoColumnLayout()
        : SingleColumnLayout(),
  );
}
```
