---
tags:
  - cheatsheet
title: Flutter
---
---
# Common Useful Widgets

- UI element : Text, Image
- Styling : BoxDecoration, TextStyle
- Layout : Container, Row, Column, Stack, Positioned, Expanded
- Lists : ListView, SingleChildScrollContainer, PageController
- Interactivity : GestureDetector
- Animation : Animation, AnimationController

# Navigation

Uses the [Navigator](https://api.flutter.dev/flutter/widgets/Navigator-class.html) class

```dart
ElevatedButton(
	onPressed: () {
	  Navigator.push(
		context,
		MaterialPageRoute(
		  builder: (context) => const ShaderHomePixelationPage(),
		),
	  );
	},
	child: const Text('Pixelation'),
)

FloatingActionButton(
  onPressed: () {
	Navigator.of(context).pop();
  },
  child: const Icon(Icons.chevron_left),
)
```

# Using Shaders

Use the CustomPainter class. This gives you access to a Canvas to which you can draw. While drawing rect, lines etc you can pass a Paint object. Paint can be passed a (fragment)shader!

### Simplest Shader in flutter

```glsl
#version 460 core

uniform vec2 uSize;
uniform vec4 uColor;

out vec4 fragColor;


void main(){
    fragColor = vec4(1.0,1.0,1.0,1.0);
}

```

# State Management

Ephemeral state can be maintained within a widget's state. For simple use cases, its alright to pass state from child widgets to parents. If the widget hierarchy is too deep and you find yourself passing state through multiple parents, consider using the `provider` package.

# IDE : Android Studio

You are constantly wrapping widgets in other widgets while building UI in flutter. Instead of doing this manually, press `Alt+Enter`. This opens up a menu from which you can choose a bunch of options :

- Wrap with Column
- Wrap with Container
- Wrap with if etc

# Concurrency and Parallelism

You can use `async/await` to do concurrent operations in your single threaded Dart VM. This is ok if none of the computation within your async/await functions are computationally intensive. To do truly parallel computation, you use `Isolates` which is something like a Thread on the Dart VM. Which uses the other free cores of your CPU.

Think of Isolates as a parallel thread you start and you communicate via messages. The APIs look like `Isolate.spawn(entry, part)` and `port.send('event_name')`

# Profiling

Run `dart --observe main.dart` and visit localhost:8181. Apparently Dart VM is constantly running some kind of profiling process and makes it available via a web UI. You can also make changes to the code via this UI and make changes to the running code without restarting the process. I don't see how this could be useful in a production setting but its very cool!
This same UI is also available to flutter in Android Studio as well.

# Uncategorized Niceties :

1. WidgetApp seems to be the parent class of MaterialApp and CupertinoApp. Should be the starting point for any true customization.

2. the `of` convention. MediaQuery.of(context) returns a MediaQueryData object. Theme.of() returns a ThemeData object.
