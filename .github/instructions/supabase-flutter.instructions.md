---
applyTo: "**/*.dart"
---

# Supabase Integration Guide

## 🚀 Quick Setup

### 1. Add Dependencies

```yaml
# pubspec.yaml
dependencies:
  flutter:
    sdk: flutter
  supabase_flutter: ^2.3.0
  provider: ^6.1.0
```

### 2. Initialize Supabase

```dart
// main.dart
import 'package:flutter/material.dart';
import 'package:supabase_flutter/supabase_flutter.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();

  await Supabase.initialize(
    url: 'YOUR_SUPABASE_URL',
    anonKey: 'YOUR_SUPABASE_ANON_KEY',
  );

  runApp(const MyApp());
}

// Global accessor for Supabase client
final supabase = Supabase.instance.client;
```

## 📋 Common Operations

### Fetching Data (SELECT)

```dart
// Fetch all posts
Future<List<Post>> fetchPosts() async {
  final response = await supabase
      .from('posts')
      .select()
      .order('created_at', ascending: false);
  
  return (response as List).map((json) => Post.fromJson(json)).toList();
}

// Fetch single post by ID
Future<Post> fetchPost(String id) async {
  final response = await supabase
      .from('posts')
      .select()
      .eq('id', id)
      .single();
  
  return Post.fromJson(response);
}

// Fetch with filters
Future<List<Post>> fetchUserPosts(String userId) async {
  final response = await supabase
      .from('posts')
      .select()
      .eq('user_id', userId)
      .order('created_at', ascending: false);
  
  return (response as List).map((json) => Post.fromJson(json)).toList();
}
```

### Creating Data (INSERT)

```dart
Future<Post> createPost({
  required String title,
  required String content,
}) async {
  final response = await supabase
      .from('posts')
      .insert({
        'title': title,
        'content': content,
        'user_id': supabase.auth.currentUser?.id,
      })
      .select()
      .single();
  
  return Post.fromJson(response);
}
```

### Updating Data (UPDATE)

```dart
Future<Post> updatePost({
  required String id,
  required String title,
  required String content,
}) async {
  final response = await supabase
      .from('posts')
      .update({
        'title': title,
        'content': content,
        'updated_at': DateTime.now().toIso8601String(),
      })
      .eq('id', id)
      .select()
      .single();
  
  return Post.fromJson(response);
}
```

### Deleting Data (DELETE)

```dart
Future<void> deletePost(String id) async {
  await supabase
      .from('posts')
      .delete()
      .eq('id', id);
}
```

## 🔐 Authentication

### Sign Up

```dart
Future<void> signUp({
  required String email,
  required String password,
}) async {
  await supabase.auth.signUp(
    email: email,
    password: password,
  );
}
```

### Sign In

```dart
Future<void> signIn({
  required String email,
  required String password,
}) async {
  await supabase.auth.signInWithPassword(
    email: email,
    password: password,
  );
}
```

### Sign Out

```dart
Future<void> signOut() async {
  await supabase.auth.signOut();
}
```

### Listen to Auth Changes

```dart
class AuthProvider extends ChangeNotifier {
  User? _user;
  
  User? get user => _user;
  bool get isAuthenticated => _user != null;

  AuthProvider() {
    _user = supabase.auth.currentUser;
    
    supabase.auth.onAuthStateChange.listen((data) {
      _user = data.session?.user;
      notifyListeners();
    });
  }
}
```

## 🔄 Real-time Subscriptions

```dart
class PostsProvider extends ChangeNotifier {
  List<Post> _posts = [];
  RealtimeChannel? _channel;

  List<Post> get posts => _posts;

  void subscribeToUpdates() {
    _channel = supabase
        .channel('public:posts')
        .onPostgresChanges(
          event: PostgresChangeEvent.all,
          schema: 'public',
          table: 'posts',
          callback: (payload) {
            // Refresh posts when changes occur
            fetchPosts();
          },
        )
        .subscribe();
  }

  @override
  void dispose() {
    _channel?.unsubscribe();
    super.dispose();
  }
}
```

## 📁 Model Pattern

```dart
class Post {
  final String id;
  final String title;
  final String content;
  final String userId;
  final DateTime createdAt;
  final DateTime? updatedAt;

  const Post({
    required this.id,
    required this.title,
    required this.content,
    required this.userId,
    required this.createdAt,
    this.updatedAt,
  });

  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      id: json['id'] as String,
      title: json['title'] as String,
      content: json['content'] as String,
      userId: json['user_id'] as String,
      createdAt: DateTime.parse(json['created_at'] as String),
      updatedAt: json['updated_at'] != null 
          ? DateTime.parse(json['updated_at'] as String)
          : null,
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'title': title,
      'content': content,
      'user_id': userId,
      'created_at': createdAt.toIso8601String(),
      'updated_at': updatedAt?.toIso8601String(),
    };
  }
}
```

## 🏗️ Provider with Supabase

```dart
class PostsProvider extends ChangeNotifier {
  List<Post> _posts = [];
  bool _isLoading = false;
  String? _error;

  List<Post> get posts => _posts;
  bool get isLoading => _isLoading;
  String? get error => _error;

  Future<void> fetchPosts() async {
    _isLoading = true;
    _error = null;
    notifyListeners();

    try {
      final response = await supabase
          .from('posts')
          .select()
          .order('created_at', ascending: false);
      
      _posts = (response as List)
          .map((json) => Post.fromJson(json))
          .toList();
    } catch (e) {
      _error = e.toString();
    } finally {
      _isLoading = false;
      notifyListeners();
    }
  }

  Future<void> createPost({
    required String title,
    required String content,
  }) async {
    try {
      final response = await supabase
          .from('posts')
          .insert({
            'title': title,
            'content': content,
          })
          .select()
          .single();
      
      _posts.insert(0, Post.fromJson(response));
      notifyListeners();
    } catch (e) {
      _error = e.toString();
      notifyListeners();
      rethrow;
    }
  }

  Future<void> deletePost(String id) async {
    try {
      await supabase.from('posts').delete().eq('id', id);
      _posts.removeWhere((post) => post.id == id);
      notifyListeners();
    } catch (e) {
      _error = e.toString();
      notifyListeners();
      rethrow;
    }
  }
}
```

## ⚠️ Error Handling

```dart
Future<void> safeSupabaseCall() async {
  try {
    await supabase.from('posts').select();
  } on AuthException catch (e) {
    // Handle auth errors (invalid credentials, expired session)
    print('Auth error: ${e.message}');
  } on PostgrestException catch (e) {
    // Handle database errors (constraint violations, permissions)
    print('Database error: ${e.message}');
  } catch (e) {
    // Handle other errors (network, etc.)
    print('Error: $e');
  }
}
```

## 📋 Quick Reference

| Operation | Method |
|-----------|--------|
| Fetch all | `.from('table').select()` |
| Fetch one | `.from('table').select().eq('id', id).single()` |
| Create | `.from('table').insert({...}).select().single()` |
| Update | `.from('table').update({...}).eq('id', id)` |
| Delete | `.from('table').delete().eq('id', id)` |
| Filter | `.eq()`, `.neq()`, `.gt()`, `.lt()`, `.like()` |
| Order | `.order('column', ascending: false)` |
| Limit | `.limit(10)` |
| Range | `.range(0, 9)` |
