---
title: Add Gestures
---

import SnackInline from '~/components/plugins/SnackInline';
import ImageSpotlight from '~/components/plugins/ImageSpotlight';
import { Terminal } from '~/ui/components/Snippet';

Gestures are a great way to provide an intuitive user experience in an application. [React Native Gesture Handler library](https://docs.swmansion.com/react-native-gesture-handler/docs/) provides a way for built-in native components that can handle gestures. It uses a platform's native touch handling system for recognizing pan, tap and rotation and other gestures.

> **Note**: React Native provides a [gesture responder system](https://reactnative.dev/docs/gesture-responder-system) that manages the lifecycle of touch events and gesture recognizers. However, it doesn't help addressing performance issues since the gesture system runs on the JavaScript thread. React Native Gesture Handler library solves this issue since it runs on the UI thread. For more information on learning differences between JavaScript thread and UI thread, see [React Native performance](https://reactnative.dev/docs/performance).

In this module, you are going to add two different gestures using React Native Gesture Handler library:

- Tap to scale the size of the sticker on double tap.
- Pan to move the sticker around the screen so that the sticker is placed anywhere on the image

## Step 1: Install libraries

To use React Native Gesture Handler library, you need to install the following libraries:

- [react-native-gesture-handler]
- [react-native-reanimated]

The `react-native-reanimated` works seamlessly with the `react-native-gesture-handler` library to create smooth animations and interactions.

To install these libraries, run the following command:

<Terminal cmd={['$ npx expo install react-native-gesture-handler react-native-reanimated']} />

The `react-native-reanimated` library requires a configuration step:

- Open `babel.config.js` file in the root of the project.
- Add `react-native-reanimated` to the `plugins` array.

<!-- prettier-ignore -->
```js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ["babel-preset-expo"],
    /* @info */
    plugins: ["react-native-reanimated/plugin"],
    /* @end */
  };
};
```

## Step 2: Enable gesture interactions

To make sure gesture interactions work in the app, you need to use `GestureHandlerRootView` from `react-native-gesture-handler` to wrap the rest of the application's code. This is done by replacing the root level `View` component in **App.js** with `GestureHandlerRootView`.

<!-- prettier-ignore -->
```js
import { GestureHandlerRootView } from "react-native-gesture-handler";

export default function App() {
  return (
    return (
    <GestureHandlerRootView style={styles.container}>
    /* rest of the code */
    </GestureHandlerRootView>
  )
}
```

Now, when you use the gesture handlers from `react-native-gesture-handler` library, they will work seamlessly.

## Step 3: Add the tap Gesture

A tap gesture recognizes one or more taps on a device's screen. React Native Gesture Handler library provides `TapGestureHandler` for tap interactions.

Start by importing `TapGestureHandler` from `react-native-gesture-handler` and hooks from `react-native-reanimated` in the **components/EmojiSticker.js** file:

```js
import { TapGestureHandler } from 'react-native-gesture-handler';
import Animated, {
  useAnimatedStyle,
  useSharedValue,
  useAnimatedGestureHandler,
  withSpring,
} from 'react-native-reanimated';
```

Then, inside the `EmojiSticker` component, create a reference called `scaleImage` using `useSharedValue` hook. This hook will take the value of `imageSize` as an initial value.

```js
const scaleImage = useSharedValue(imageSize);
```

Using a shared value created using `useSharedValue` hook has many advantages. Apart from mutating as a shared piece of data, it allows running animations based on the current value. A shared value can be accessed and modified using the `.value` property. We will use this to scale the initial value fo `scaleImage` so that when a user double taps the sticker, it scales to twice its original size. We will do it by creating a handler method called `tapGestureHandler` that uses `useAnimatedGestureHandler` hook to allow us to animate the transition during the process of scaling the sticker image.

```js
const tapGestureHandler = useAnimatedGestureHandler({
  onActive: () => {
    if (scaleImage.value) {
      scaleImage.value = scaleImage.value * 2;
    }
  },
});
```

We will use `withSpring` which is a built-in animation provided by `react-native-reanimated` to create a spring animation. This animation will be used to scale the sticker image when a user double taps it. We will also use `useAnimatedStyle` hook to create a style object that will be applied to the sticker image to update the initial values with shared values when the animation happens.

```js
const imageStyle = useAnimatedStyle(() => {
  return {
    width: withSpring(scaleImage.value),
    height: withSpring(scaleImage.value),
  };
});
```

Next, wrap the `Image` component that displays the sticker on the screen with `TapGestureHandler` component.

```js
return (
  <View style={{ top: -350 }}>
    <TapGestureHandler onGestureEvent={tapGestureHandler} numberOfTaps={2}>
      <AnimatedImage
        source={stickerSource}
        resizeMode="contain"
        style={[imageStyle, { width: imageSize, height: imageSize }]}
      />
    </TapGestureHandler>
  </View>
);
```

To scale the image, we need to scale the width and height of the image. The `scaleImage` reference is used to scale the image.
