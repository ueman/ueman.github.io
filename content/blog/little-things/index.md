---

title: "Improving the little things"

date: 2023-03-11T10:00:00+02:00

---

# Improving the little things

In this blog post you'll learn which small changes you can do for your app, in order to create a better experience for your users.
We're focussing on Flutter apps for Android and iOS.

## Acoustic and haptic feedback for a better UX


more interactive feedback https://twitter.com/ue_man/status/1632848634051014656?t=2-kch4D6078MC81JtKz01Q&s=19

https://twitter.com/ue_man/status/1632717439531114498?t=822dhNuKIUfqZ5UYfpxmRg&s=19


## Edge to edge mode (Android)

The first tip is to enable the so-called edge to edge mode for Android.

| before | after |
|:-:|:-:|
|![](e2e-before.png)|![](e2e-after.png)|

As you can see in the before screenshot, the app has an iOS-like swipe indicator on a black bar.
By enabling the edge to edge mode, we also show content behind this indicator.
In order to do this you just change your code from 

```dart
void main() {
  runApp(const MyApp());
}
```

to the following code

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  SystemChrome.setSystemUIOverlayStyle(
    const SystemUiOverlayStyle(systemNavigationBarColor: Colors.transparent),
  );
  await SystemChrome.setEnabledSystemUIMode(SystemUiMode.edgeToEdge);
  runApp(const MyApp());
}
```

This should be a painless migration, because your code should already be properly adapted to this, since it's the default behavior on newer iOS devices.

Please be aware though, that this might cause issues on older Android versions. There's also a [Flutter issue](https://github.com/flutter/flutter/issues/86248) to make this the default behavior for newly generated Flutter versions.

## High refresh rate (Android)

Flutter apps are making use of high refresh rates by default on iOS. On Android, however, it isn't that easy. Different manufactures mess with the system and can disable the automatic enabling of high refresh rate.
One Plus, Oppo and Nothing for example do this. Xiaomi doesn't.
You can force a high refresh rates to a certain degree by using [display_mode](https://pub.dev/packages/flutter_displaymode).

Add the package as a dependency and change your code from

```dart
void main() {
  runApp(const MyApp());
}
```

to the following code

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await FlutterDisplayMode.setHighRefreshRate();

  runApp(const MyApp());
}
```

Congratulations, your app runs now at a high refresh rate in most cases.