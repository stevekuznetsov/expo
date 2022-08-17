---
title: Add Gestures
---

import SnackInline from '~/components/plugins/SnackInline';
import ImageSpotlight from '~/components/plugins/ImageSpotlight';
import { Terminal } from '~/ui/components/Snippet';

Gestures are a great way to provide an intuitive user experience in an application. [React Native Gesture Handler library](https://docs.swmansion.com/react-native-gesture-handler/docs/) provides a way for built-in native components that can handle gestures. It uses a platform's native touch handling system for recognizing pan, tap and rotation and other gestures.

> **Note**: React Native provides a [gesture responder system](https://reactnative.dev/docs/gesture-responder-system) that manages the lifecycle of touch events and gesture recognizers. However, it doesn't help addressing performance issues since the gesture system runs on the JavaScript thread. React Native Gesture Handler library solves this issue since it runs on the UI thread. For more information on learning differences between JavaScript thread and UI thread, see [React Native performance](https://reactnative.dev/docs/performance).

In this module, you are going to add two different gestures using React Native Gesture Handler library:

- Tap to scale the size of the sticker on double tapping the sticker.
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

## Step 2: Add the tap Gesture

The tap gesture is going to allow the user to double tap the sticker to scale it up. Initially,
